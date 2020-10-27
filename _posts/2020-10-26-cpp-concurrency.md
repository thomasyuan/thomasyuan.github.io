---
title: "C++ Concurrency"
excerpt_separator: "<!--more-->"
toc: true
categories:
  - Blog
tags:
  - C++
  - Concurrency
---

> https://www.youtube.com/watch?v=F6Ipn7gCOsY

## What is concurrency?

* Concurrency means doing two things concurrently — “running together.” Maybe you’re switching back and forth between them.
  * Writing slides and answering email
* Parallelism means doing two things in parallel — simultaneously.
  * Writing slides and listening to music
* In extremely broad strokes, parallelism is a hardware problem(think multiple CPUs) and concurrency is a software problem (think time-sharing, but also Intel’s “hyperthreading”).

### Standard C++03 didn’t have “threads.” 
* The compiler can rewrite accesses
* The hardware can reorder accesses
### C++11 gave us a “memory model”
* Now a program consists of one or more threads of execution
* Every write to a single memory location must synchronize-with all other reads or writes of that memory location, or else the program has undefined behavior
* Synchronizes-with relationships can be established by using various standard library facilities, such as std::mutex and std::atomic<T>

## C++11
### std::mutex
```c++
class TokenPool {
    std::mutex mtx_;
    std::vector<Token> tokens_;
    Token getToken() {
        mtx_.lock();
        if (tokens_.empty())
            tokens_.push_back(Token::create());
        Token t = std::move(tokens_.back());
        tokens_.pop_back();
        mtx_.unlock();
        return t;
    }
};
```

BUT, It's not exception safe! use RAII lock_guard or unique_guard

### std::lock_guard && std::unique_guard
* lock_guard has better performance
* unique_guard is more flexiable (can manually lock and unlock, and lazy initialization)
* lock_guard can't pass around (not copyable and moveable)
* unique_guard is moveable

### std::lock
Locks the given Lockable objects lock1, lock2, ..., lockn using a deadlock avoidance algorithm to avoid deadlock.
> https://en.cppreference.com/w/cpp/thread/lock

```
        std::lock(e1.m, e2.m);
        std::lock_guard<std::mutex> lk1(e1.m, std::adopt_lock); // e1.m is already locked, the lock_guard with adopt_lock is used for exception-safe
        std::lock_guard<std::mutex> lk2(e2.m, std::adopt_lock);
// Equivalent code (if unique_locks are needed, e.g. for condition variables)
//        std::unique_lock<std::mutex> lk1(e1.m, std::defer_lock); // defer_lock does not lock the associated mutex
//        std::unique_lock<std::mutex> lk2(e2.m, std::defer_lock);
//        std::lock(lk1, lk2);                                     // lock the mutex here.
// Superior solution available in C++17
//        std::scoped_lock lk(e1.m, e2.m);

```

### std::condition_variable
```c++
struct TokenPool {
    std::vector<Token> tokens_;
    std::mutex mtx_;
    std::condition_variable cv_;
    void returnToken(Token t) {
        std::unique_lock lk(mtx_);
        tokens_.push_back(t);
        lk.unlock();
        cv_.notify_one();
    }
 
    Token getToken() {
        std::unique_lock lk(mtx_);
        while (tokens_.empty()) {
            cv_.wait(lk);
        }
        Token t = std::move(tokens_.back());
        tokens_.pop_back();
        return t;
    }
};
```

Note:
```c++
    while (tokens_.empty()) {
        cv_.wait(lk);
    }
```

can be replaced by 
```
    cv.wait(lk, []() { return !tokens_.empty(); });
```
> https://en.cppreference.com/w/cpp/thread/condition_variable/wait


### Thread-safe static initialization
* In C++03, to make a “singleton” thread-safe, you had to experiment with things like “double-checked locking,” and of course it was all UB anyway.
* In C++11, it’s as easy as:
```c++
inline auto& SingletonFoo::getInstance() {
    static SingletonFoo instance;
    return instance;
}
```

The first thread to arrive will start initializing the static instance. Any more that arrive will block and wait until the first thread either succeeds (unblocking them all) or fails with an exception (unblocking one of them).

### Initialize a member with once_flag
```c++
class Logger {
    std::once_flag once_;
    std::optional<NetworkConnection> conn_;
    NetworkConnection& getConn() {
        std::call_once(once_, []() {
            conn_ = NetworkConnection(defaultHost);
        });
        return *conn_;
    }
};
```

It's better than mutex solution because you don't need lock everytime. (the initialized only called onece)
```c++
class Logger {
    std::mutex mtx_;
    std::optional<NetworkConnection> conn_;
    NetworkConnection& getConn() {
        std::lock_guard<std::mutex> lk(mtx_);
        if (!conn_.has_value()) {
            conn_ = NetworkConnection(defaultHost);
        }
        return *conn_;
    }
};
```

### promise/future/async
> https://www.youtube.com/watch?v=SZQ6-pf-5Us&list=RDCMUCEOGtxYTB6vo6MQ-WQ9W_nQ&index=6
* async call a function to in async way and return a future
  * std::launch::async	a new thread is launched to execute the task asynchronously
  * std::launch::deferred	the task is executed on the calling thread the first time its result is requested (lazy evaluation)
* future.get() will wait there until the async task finished.

```c++
/* Asynchronously provide data with promise */
int factorial(future<int>& f) {
	// do something else
	int N = f.get();     // If promise is distroyed, exception: std::future_errc::broken_promise
	cout << "Got from parent: " << N << endl; 
	int res = 1;
	for (int i=N; i>1; i--)
		res *= i;

	return res;
}

int main() {
	promise<int> p;
	future<int> f = p.get_future();

	future<int> fu = std::async(std::launch::async, factorial, std::ref(f));

	// Do something else
	std::this_thread::sleep_for(chrono::milliseconds(20));
	p.set_value(5);   

	cout << "Got from child thread #: " << fu.get() << endl;
	return 0;
}
```
  



## C++17
### std::scoped_guard (c++17)
An alternative for std::lock, and much more simpler.

### std::shared_mutex (R/W lock)
The shared_mutex class is a synchronization primitive that can be used to protect shared data from being simultaneously accessed by multiple threads. In contrast to other mutex types which facilitate exclusive access, a shared_mutex has two levels of access:
* shared - several threads can share ownership of the same mutex.
* exclusive - only one thread can own the mutex.

```c++
class ThreadSafeConfig {
    std::map<std::string, int> settings_;
    mutable std::shared_mutex rw_;
    
    void set(const std::string& name, int value) {
        std::unique_lock<std::shared_mutex> lk(rw_);
        settings_.insert_or_assign(name, value);
    }
    
    int get(const std::string& name) const {
        std::shared_lock<std::shared_mutex> lk(rw_);
        return settings_.at(name);
    }
};
```

## C++20

### std::counting_semaphore

### std::latch
A latch is kind of like a semaphore, in that it has an integer counter that starts positive and counts down toward zero.
* latch.wait() blocks until the counter reaches zero.
* latch.count_down() decrements the counter.
  * If the counter reaches zero then this unblocks all the waiters.
* latch.arrive_and_wait() decrements and begins waiting.

Use a std::latch as a one-shot “starting gate” mechanism: “Wait for everyone to arrive at this point, then unblock everyone simultaneously.”
latch is like once_flag in that there is no way to “reset” its counter.


```c++
    std::latch myLatch(1);
    std::thread threadB = std::thread([&](){
      myLatch.wait();
      printf("Hello from B\n");
    });
    
    printf("Hello from A\n");
    myLatch.count_down();
    threadB.join();
    printf("Hello again from A\n");
```



### std::barrier


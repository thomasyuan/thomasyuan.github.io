---
title: "Lesson Learned - Java Timer"
excerpt_separator: "<!--more-->"
toc: true
categories:
  - Blog
tags:
  - Lesson Learned
  - Java
  - Timer
---

## Issue

When you use Java Timer (java.util.Timer) to set a task in future, you should be really careful. Java Timer use currentTimeMillis, which will be affected by system clock.
> https://github.com/openjdk-mirror/jdk7u-jdk/blob/master/src/share/classes/java/util/Timer.java


If you want to start a one time timer, you can call `schedule(TimerTask task, long delay)`, here is the sample code.

```java
import java.util.Timer;
import java.util.TimerTask;

public class TimerTest {
	static Timer timer;
	public static void main(String[] args) {
		timer = new Timer();
		timer.schedule(new TimerTask(){

			@Override
			public void run() {
				System.out.println(Thread.currentThread().getId() + " Time's up!");
				timer.cancel();
			}
		}, 3000);

		System.out.println(Thread.currentThread().getId() + " Timer scheduled.");
	}
}

```

When you run the code, if should print out something like this
```
1 Timer scheduled.
12 Time's up!
```
It takes about 3 seconds to finish since the delay is set to 3000 milliseconds.

But what if you change the system clock just after you run the code? The result is, if you change the system back to 10 minutes before, then you have to wait 10 minutes + 3 seconds to get the timeout message.

The even worse case is for repeated timer. like `scheduleAtFixedRate(TimerTask task, long delay, long period)`. When you change the system clock to the future, the timer will try to catch up the time, then the timer task will be executed continuously, which might take all your CPU cycles.


> https://bugs.openjdk.java.net/browse/JDK-4290274

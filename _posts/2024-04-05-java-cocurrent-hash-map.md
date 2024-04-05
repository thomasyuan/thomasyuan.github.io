---
title: "Java Note"
excerpt_separator: "<!--more-->"
toc: true
categories:
  - Blog
tags:
  - Java
  - cocurrentHashMap
---


ConcurrentHashMap is designed to support concurrent access from multiple threads without the need for external synchronization. It achieves this by using various strategies such as partitioning the map into segments and utilizing fine-grained locking.

Here's how ConcurrentHashMap handles different operations:

- Insertion (put, putIfAbsent): Insertion operations are thread-safe in ConcurrentHashMap. You don't need external locks to safely insert elements into the map. Internally, it uses locking mechanisms only at the segment level or sometimes finer-grained locks for better concurrency.
- Removal (remove): Similar to insertion, removal operations are also thread-safe. You can safely remove elements from the map concurrently without external locks.
- Iteration (Iterator): Iterating over a ConcurrentHashMap using its Iterator is also safe. The iterator returned by ConcurrentHashMap is weakly consistent, meaning it reflects some, but not necessarily all, of the changes that have been made to the map since the iterator was created. It does not throw ConcurrentModificationException as in the case of traditional HashMap.

However, it's important to note that even though ConcurrentHashMap **provides thread-safety for individual operations, compound actions (like iterating through the map while modifying it) may not be atomic**. If you need compound actions to be atomic, you should use additional synchronization mechanisms.

In summary, for basic operations like insertion, removal, and iteration, you generally don't need external locks when using ConcurrentHashMap.

Guess what's output of below code.
```java
import java.util.concurrent.ConcurrentHashMap;
import java.util.Map;

public class Main {
    public static void main(String[] args) {
        ConcurrentHashMap<Integer, String> map = new ConcurrentHashMap<>();
        map.put(1, "One");
        map.put(2, "Two");
        map.put(3, "Three");

        // Modifying the map concurrently while iterating using for-each loop
        for (Map.Entry<Integer, String> entry : map.entrySet()) {
            System.out.println(entry.getValue());
            // if (entry.getKey() == 1) {
            //     map.remove(3);
            // }
            if (entry.getKey() == 2) {
                map.put(4, "Four");
            }
            if (entry.getKey() == 4) {
                map.remove(1);
            }
        }
        System.out.println();
        for (Integer key : map.keySet()) {
            System.out.println(map.get(key));
        }
    }
}
```

on https://www.programiz.com/java-programming/online-compiler/, the result is
```
One
Two
Three
Four

Two
Three
Four
```
All seems working fine.

if uncomment out the logic `map.remove(3)` in the loop, then 
The the output is
```
One
Two

One
Two
Four
```
From the code, 3 and 1 should be removed, 4 should be added, so the expected the result `should` be
- First round: ONE TWO FOUR
- Second round: TWO FOUR

Both of the expections are wrong. at the end, the item <1, "ONE"> is still in the map!





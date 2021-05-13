---
title: "Java - Volatile or Synchronized"
excerpt_separator: "<!--more-->"
toc: true
categories:
  - Blog
tags:
  - Java
  - Concurrency
---

## Volatile

There are two features when talking about thread-safe (Concurrency)

- Mutual Exclusion: It means that only one thread or process can execute a block of code (critical section) at a time.
- Visibility: It means that changes made by one thread to shared data are visible to other threads.

The synchronized keyword fixes all these, but if you just want Visibility, then you can use volatile.

> Reference https://www.geeksforgeeks.org/volatile-keyword-in-java/

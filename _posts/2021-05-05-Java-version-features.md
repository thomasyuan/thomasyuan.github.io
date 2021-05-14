---
title: "Java Features By Version"
excerpt_separator: "<!--more-->"
toc: true
categories:
  - Blog
tags:
  - Java
---

## Java 8

> https://www.oracle.com/java/technologies/javase/8-whats-new.html

- Functional Interfaces and Lambda Expressions
- Default and static methods in Interfaces.

* for example, forEach() default implemention in Iterable interface

```java
	default void forEach(Consumer<? super T> action) {
      Objects.requireNonNull(action);
      for (T t : this) {
          action.accept(t);
      }
  }
```

- Method references provide easy-to-read lambda expressions for methods that already have a name.
- Java Stream
  - `java.util.stream` package provide a Stream API to support functional-style operations on streams of elements. The Stream API is integrated into the Collections API, which enables bulk operations on collections, such as sequential or parallel map-reduce transformations.
- Java Date-Time Packages
  - `java.time` - Classes for date, time, date and time combined, time zones, instants, duration, and clocks.
  - `java.time.chrono` - API for representing calendar systems other than ISO-8601. Several predefined chronologies are provided and you can also define your own chronology.
  - `java.time.format` - Classes for formatting and parsing dates and time.
  - `java.time.temporal` - Extended API, primarily for framework and library writers, allowing interoperations between the date and time classes, querying, and adjustment. Fields and units are defined in this package.
  - `java.time.zone` - Classes that support time zones, offsets from time zones, and time zone rules.
- Concurrency Utilities Enhancements
- Java IO improvements

## Java 9

> https://docs.oracle.com/javase/9/whatsnew/toc.htm#JSNEW-GUID-DB9EB298-4944-4BF9-9CE0-B4A884F8294F

- Introduces module
- Introduces jshell
- Add support for private interface methods.

## Java 10

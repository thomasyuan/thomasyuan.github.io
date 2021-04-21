---
title: "Java SE: Programming Complete - 3"
excerpt_separator: "<!--more-->"
toc: true
categories:
  - Blog
tags:
  - Java
  - Certificate
  - OCP
---

> https://learn.oracle.com/ols/course/java-se-programming-complete/82508/85200

## Text, Date, Time and Numberic Objects

#### String

* String is a class (not a primitive), can be instantiated by using the `new` keyword.
* However, String is the only Java object that allows simplified instantiation as a text value enclosed with double quotes, and it's a recommened approach.
* JVM can optimize memory allocated to store String objects by maintaining **a single copy of each String literal** in the String Pool memory area, **regardless of how many variables reference this copy** (This process is called interning)
* Using `new` keyword disables String interning.
* The intern() method returns a reference to an interned (single) copy of a String literal.
```java
  String a = new String("Hello");
  String b = new String("Hello");
  String c = "Hello";
  String d = "Hello";
  System.out.println(a == b);       // false
  System.out.println(a.intern() == b.intern());   // true
  System.out.println(c == d);       // true
```
* String is immutable, String operations such as `trim()`, `contact()`, `toLowerCase()`, `toUpperCase()` ould always return a new String, would not modify the original String.
* String contains a sequence character indexed by integer, starts from 0.
* When getting a `substring` of a string, the begin index is inclusive of the result, but end index is out.

#### StringBuilder
* StringBuilder is mutable, allowing modifcation of the character sequences they store.

#### Wrapper Classes for Primitives
* Wrapper classes apply object-oriented capabilities to primitives.
* Construct wrapper object out of primitive or string using the `valueOf()` methods
* Extract primitive values out fo the wrapper using the `xxxValue()` methods.
* Instead of formal conversion of wrapper to primitive and back, you can use direct assignment known as auto-boxing and auto-unboxing
* Create wrapper of primitive out of the string using the parseXXX() methods: `float f = strObj.parseFloat(1.23F)`
* Convert a primitive to string using the `String.valueOf()` method: `String strObj = String.valueOf(3)`
* Wrapper classes provide constants, such as min and max values for every type. for example `Short.MIN_VALUE`

#### Representing Numbers Using `BigDecimal` Class
* The `java.math.BigDecimal` class is useful in handling decimal numbers that require exact precision

#### Method Chaining
* When an operation returns an object, you may invoke next operation upon this object immediately.
* Without method chainning, code appears to be cluttered with *unnecessary intermediate variables*

#### LOcal Date and Time
* Classes `LocalDate`, `LocalTime` and `LocalDateTime` are introduced in Java SE 8, to address the shortcomings of the older java.util.Date and java.util.Calendar. (Thread Safety, API design and timezone)
* Date and time objects can be created using methods `now()` to get current date and time, or using `of()` for specific date and time.
* Local Date and Time objects are **immutable**
* Operations `isBefore()` and `isAfter()` check if a date or time is before or after another.

#### Durations, Periods and Instants
* The `java.time.Duration` class can represent an anoumnt of time in nanoseconds.
* The `java.time.Period` class can represent an amount of time in units such as years or days.
* The `java.time.Instant` class can represent an instantaneous point on the time-line (time-stamp)
* `Duration`, `Period` and `Instant` are **immutable**.

#### Zoned Date and Time
* Time zones can be applied to local date and time values `java.time.ZonedDateTime`




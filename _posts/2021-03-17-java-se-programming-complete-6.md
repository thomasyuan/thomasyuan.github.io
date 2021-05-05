---
title: "Java SE: Programming Complete - 6"
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

## Inheritance

#### Extend Classes
- `java.lang.Object` is an ultimate paraent of any other class in Java
- A class can have only one immediate parent, as multiple inheritance is not allow in Java 
- `Object` defines common, generic operations that all other Java classes inherit and reuse:
 * The `toString` method creates teext value for the object
 * The `equals` method compares a pair of objects
 * The `hashCode` method generates int hash value for the object.
 * The `clone` method produces a replica of the object.
 * `wait`, `notify` and `notifyAll` methods control threads.

#### Reuse Parent Class Code Through Inheritance
- The purpose of inheritance is to reuse generic superclass behaviors and state in subclass

#### Instantiating Classes and Accessing Objects
- Heap memory allocated to store object (class instance) that contians
 * Code of the specific subtype
 * All of the parents up the class hierarchy
- Object reference can be of generic or specific type
  ```java
  public class Product {}
  public class Food extends Product {}

  Object x1 = new Food();
  Product x2 = new Food();
  Food x3 = new Food();
  ```
  In this example, 
  * x1 can only access code declared on the Object class
  * x2 can access Object and Product 
  * x3 can access Object, Product and Food.

#### Rules of Reference Type Casting
- Casting is required to assign parent to child reference type.
- No casting is required to assign child to parent reference type
- Use `instanceof` operator before casting reference from generic to specific type.


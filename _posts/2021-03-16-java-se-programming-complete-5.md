---
title: "Java SE: Programming Complete - 5"
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

## Improved Class Design

#### Use Method Overloading

- Two or more methods, with the same class, that have identical names.
- Must have a different number, or different types, or different order of parameters, return type doesn't count, compile error.
- To make it easier for caller to make the call.

#### Variable Number of Arguments

- The vararg feature enables a variable number of arguments of the same types
- The vararg parameter is treated as an array, with the `length` constant indicating a number of values.
- In case where there are other parameters in the method, the vararg parameter must be defined last.

```java
class example {
  public static void main(String[] args) {}
  // Or
  // public static void main(String... args) {}
}
```

#### Define Constructors

- Same name as the class name, no return type.
- A default constructor with no parameters is implicitly added to the class, **only if no other constructors were added**
- A constructor can invoke another to reuse its logic, by using keyword `this(other constructor parameters);`, and it must be the first line of code in the nvoking constructor.
- A cycle of constructor invocations is not allowed.

#### Access Modifiers

- public - visible to any class
- protected - visible to subclasses and class in same package
- <default> - visible to class in smae package
- private - visible within the same class only

#### Define Encapsulation

- Information contained within the object should normally be "hidden" inside it.
- Use access modifiers properly to control access

#### Define Immutability

- Immutability objects present read-only data.
- Instance variables must be encapsulated (private) to prevent direct access.
- Instance variables are initialized immediately or via constructors (use `final` or not).
- No setter mothods, only getter.
- Benifit, immutable objects are thread-safe, without an overhead cost of coordinating synchronized access.
- Instance initializer (compare static initializer, no `static` keyword) is triggered **before** the invocation of the constructor, can initialize `final` instance variable.

#### Enumerations

- Enumeration (enum) provides a **fixed** set of instances of a specific type
- Enum values are instances of this enum type.
- Enum values are implicitly `public static final`
- Enum can define instance variables and methods.
- A constructor should be added to the enumeration to initialized its instance variables.
- The constructor for an enum must have `default` or `private` access
- Declaration of enum values invokes the enum constructor.
- The enum constructor can be invoked outside of enum.

#### Java Memory

- Stack is a memory context of a thread, storing local method variable: primitives or object reference
- Heap is shared memory, accessible from different method and thread contexts.
- parameter passing means copying stack values.
- Garbage collection will clean object when there are no reference pointing to it

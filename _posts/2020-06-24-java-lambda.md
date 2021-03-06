---
title: "Java - Lambda"
excerpt_separator: "<!--more-->"
toc: true
categories:
  - Blog
tags:
  - Java
  - Lambda
---

## Lambda

Before Java SE 8, anonymous classes were typically used to pass functionality to
a method. This practice obfuscated source code, making it harder to understand.
Java 8 eliminated this problem by introducing lambdas.

Lambdas simplify the use of **_functional interfaces_**, which are annotated
interfaces that each declare exactly **one abstract method** (although they can
also declare any combination of default, static, and private methods). One example
is `java.lang.Runnable` interface from the standard class library. It only has single
method which is `abstract void run()`.

Another good example of function interface

```java
@FunctionalInterface
public interface FucnctionalDemo {

  void letsDoSomething();
  //void letsGo();      //invalid because another abstract method does not allow
  public String toString();    // valid because toString from Object
  public boolean equals(Object o); //valid

  public static int sum(int a,int b)   // valid because method static
  {
    return a+b;
  }
  public default int sub(int a,int b)   //valid because method default
  {
    return a-b;
  }
}
```

### Lambda syntax

Every lambda conforms to the following syntax:

```java
( formal-parameter-list ) -> { expression-or-statements }
```

> ### Lambdas and var
>
> Starting with Java SE 11, you can replace a type name with var. For example,
> you could specify (var a, var b).

### Lambdas and scopes

A lambda body doesn't introduce a new scope. Instead, its scope is the enclosing scope.

### Lambdas and local variables

A lambda body can define local variables. Because these variables are considered
part of the enclosing scope, the compiler will report an error when it detects
that the lambda body is redefining a local variable.

A local variable or parameter that's defined outside a lambda body and referenced
from the body must be marked final or considered effectively final.

### Lambdas and the 'this' and 'super' keywords

Any this or super reference that is used in a lambda body is regarded as being
equivalent to its usage in the enclosing scope (because a lambda doesn't introduce
a new scope). However, **this isn't the case with anonymous classes**.

### Lambdas and exceptions

A lambda body is not allowed to throw **_more exceptions than are specified_** in
the throws clause of the functional interface method. If a lambda body throws an
exception, the functional interface method's throws clause must declare the same
exception type or its supertype.

## Reference

- https://www.javaworld.com/article/3452018/get-started-with-lambda-expressions.html

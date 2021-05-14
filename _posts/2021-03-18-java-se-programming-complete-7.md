---
title: "Java SE: Programming Complete - 7"
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

## Interface

#### Java Interface

- An interface defines a set of features that can be applied to various other classes.
- Instance methods are by default `public` and `abstract`
- They can contain concrete methods only if they are either `default`, or `private` or `static`.
- They can contain `constant`, but not variables.
- An interface can `extends` another interface.
- Interface is a Type, just like a class.
- Interface is a valid reference type, can be used in type casting, and works with the `instanceof` operator.
- Object class is the ultimate parent type in Java, so interface is `instanceof` Object, and has `toString`, `hashCode` etc methods as well.

```java
public interface <InterfaceName> {
  <constants>
  <abstract methods>
  <default methods>
  <private methods>
  <static methods>
}
```

For example:

```java
public interface Perishable {
  public static final Period MAC_PERIOD = Period.ofDays(5);
  void perish();
  boolean isPerished();
  public default boolean verifyPeriod(Period p) {
    return comparePeriod(p) < 0;
  }
  private int comparePeriod(Period p) {
    return p.getDays() - MAX_PERIOD.getDays();
  }
  public static int getmaxPeriodDays() {
    return MAX_PERIOD.getDays();
  }
}
```

#### Multiple Inheritance Problem

- Java doesn't support multiple inheritance because that might have conflict: If two parents provide concrete operations with identical signatures or variables with identical name.
- Interface is used to fix this issue.

  - If two interface have identical signature abstract methods, since there are no implementation, no conflict
  - Same reason, since interface doesn't have variables, so not conflict.
  - Private interface methods don't cause conflicts, because they are not visible outside of the interface.
  - Static interface methods don't cause conflicts, because they are invoked via specific parent type.
  - If there is a conflict between default methods, it must be resolved by overriding this default method within the implementation class, otherwise the default method implementation can be inherited.
  - Default method can only be defined in an interface.

#### Functional Interface

- Functional interface is an interface that defines a single abstract operation (function).
- An interface with many abstract methods is not convenient to use.

#### Generics

> Generics is a feature of Java language available since Java SE 5

- It allows variables and methods to operate on objects of various types while providing compile-time type safety.
- Before Java SE 5 wrap values within the class using the type Object
- After Java SE 5 wrap values within the class, but defer the exact type identification.
- Generic type avoids hard-coding the exact type as part of the class design.
- The use of Generics helps to produce compact, type-safe code.

```Java
// Before Java SE 5
public class Some {
  private Object value;
  public Object getValue() {
    return value;
  }
  public void setValue(Object value) {
    this.value = value;
  }
}

// After Java SE 5
public class Some<T> {
  private T value;
  public T getValue() {
    return value;
  }
  public void setValue(T value) {
    this.value = value;
  }
}
```

#### Examples of Java Interface: `java.lang.Comparable`

- Comparable interface describes a way of comparing current object to another object.
  - current less than the other, return negative
  - current equal to the other, return 0
  - current greater than the other, return positive.

```java
public interface Comparable<T> {
  int compareTo(T o);
}
```

#### Examples of Java Interface: `java.util.Comparator`

- Comparator interface describes a way of comparing a pair of objects.

```java
public interface Comparator<T> {
  int compare(T o1, T o2);
}
```

#### Example of Java Interface: `java.lang.Cloneable`

- Cloneable is an example of an interface used as a `type-marker` or `tag-interface`
- The interface doesn't not have to define any methods.
- It can still be used with the `instanceof` operator to validate the object type.
- Cloning an object means creating a replica of the objects memory.
- The `java.lang.Cloneable` interface indicates a permission that an object can be cloned.

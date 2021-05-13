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

## Interface

#### Java Interface

- An interface defines a set of features that can be applied to various other classes.
- Instance methods are by default `public` and `abstract`
- They can contain concrete methods only if they are either `default`, or `private` or `static`.
- They can contain `constant`, but not variables.

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

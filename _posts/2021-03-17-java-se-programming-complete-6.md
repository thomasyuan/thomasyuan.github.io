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

#### Reference Code Within the Current or Parent Object
> You can have same name variable in parent and subclass!!! Well-encapsulated code should only expose the method,
so all variables should be private. In this case, no issues. **BUT** if the class have public/protected variable,
then the same name variable in subclass will hide the parenet one. use `this` and `super` to distinguish them.

#### Define Subclass Contructors.
- The subclass contructor must invoke the superclass constructor.
- If superclass contains the no-arg constructor (default or explicitly defined), then the subclass can implicity invoke the superclass constructor.
- If superclass doesn't provide the no-arg constructor, subclass constructor must explicitly invoke superclass constructor.
- Invocation of superclass constructor must be the first line of code in the subclass constructor.

#### Class and Object Initialization Summary
```java
public class Shop {
  static {}
  public static void main(Stringp[] args) {
    Product p1 = new Food();
  }
}

public class Object {
  static {}
  public Object() {}
}

public class Product {
  static {}
  {}
  public Production() {}
}

public class Food extends Product {
  static {}
  {}
  public Food() {}
}
```
- Class loading and initialization execution order:
(The following code is executed only once.)
 1. `Object` class static initializer. (since Object is the root class)
 2. `Shop` class static initializer
 3. `Product` class static initializer
 4. `Food` class static iniializer
> - All code of the class must be loaded into memory first.
> - It needs to be loaded only once per class
- Ojbect instantiation execution order:
 1. `Object` class onstructor
 2. `Product` instance initializer
 3. `Product` constructor
 4. `Food` instance initializer
 5. `Food` constructor.
> - Each object instance must be initialized together with all of it's parents.
> - Each object instance memory contains object data and references to the rest of the class code (shared between all instances).

#### Override Methods and Use Polymorphism
- The subclass can override parent class methods.
- The subclass can widen but can't narrow access of methods it overrides.
- Polymorphism in Java means when a method is declared in a superclass and is overridden in a subclass, the subclass method takes precedence without casting reference to specific subclass type.
- `Override` annotation is optional, it's used to ensure that subclass method signature matches the superclass method.

#### Define Abstract Classes and Methods
- Class can't be directly instantiated if it is marked with the `abstract` keyword. (Even there is no abstract method inside)
- The abstract class purpose is to be extended by one or more concrete subclasses.
- It may also contain abstract methods that describe method signatures, without a method body.

#### Define Final Classes and Methods
- The `final` keyword can be used to limit class extensibility
- Class can't extend a class that is marked with the `final` keyword
- The subclass can't override a superclass method that is marked with the `final` keyword.

#### Override Object Class Operations
- `toString()`, `equals()`, `hashCode`
- The `equals` comare objects, the `==` operator compares values in the **stack**, so either primitive value, or two references. not real data inside the object. Java classes such as `String`, `Number`, `LocalDate` override the `equals` method.
- The `hashCode` methods should return same hash code if `equals` return true for two object.
- The `hashCode` should be immutable.
- A `java.security.MessageDigest` class should be used to generate secure hash values.



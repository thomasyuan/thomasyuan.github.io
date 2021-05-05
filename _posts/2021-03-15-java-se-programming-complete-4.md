---
title: "Java SE: Programming Complete - 4"
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

## Classes and Objects

#### Designing Classes

- Description of the `package` that this class is a member fo
- Description of `imports` of classes from different packages that this class may need to reference
- This class `access modifer`, keyward `class` followed by the class name.
- Class and method bodies are enclosed with `{}`
- Uninitialized primitives are defaulted to 0, boolean to false.
- Uninitialized object references are defaulted to null.

```java
package <PackageName>;

import <PackageName>.<ClassName>;

<AccessModifer> <VariableType> <VariableName> = <VariableValue>;
<AccessModifer> <VariableType> <VariableName>;

<AccessModifer> class <ClassName> {
  <AccessModifer> <ReturnType> <MethodName>(<ParameterType> <ParameterName>, ...) {

    return <ReturnValue>
  }
}
```

#### Object Creation and Access

- The `new` operator creates an Object, allocating memory to store this object
- You may assign an object reference to a variable of the appropriate type.
- Access variable or methods of the object using `.` operator.

#### Local Variables and Recursive Object Reference

- Variables declared inside methods are known as Local.
- Method parameters are essentially local variables
- The local variable can "shadow" the instance variable if their names coincide
- Use the `this` keyword to refer to current instance.

#### Local Variable Type Inference (from Java 10)

- There is no need to describe a variable type if it can be unambiguously inferred from the context
- Inter types of local variables with initializers.
- No need to explicitly declare local variable type if it can be inferred from the assigned value.
- This feature is limited to
  - Local variables with initializers
  - Indexes in the enhanced for-loops
  - Local variables declared in a traditional for-loops
- Overuse can reduce code readability.

#### Define Constants

- Constants represent data that is assigned once and cannot be changed.
- The keyword `final` is used to make a variable as a constant.
- Instance final variable must be either initialized immediately or via all constructors. (No default value here, because why you need a variable if it's always default value?)

#### Static Context

- Each **Class** has its own memory context
- Class memory context (also known as static context) is shared by all instances of this class
- The keyword `static` is ued to mark variables or methods that belong to the class context.
- Attempt to access current instance methods or variable from the static context will result in compiler error.
- Static initializer runs once, before any other operation (when class is loaded)

  ```java
  class example {
    static {
      xxxx
    }
  }

  ```

####

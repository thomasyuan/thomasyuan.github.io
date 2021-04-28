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
* Description of the `package` that this class is a member fo
* Description of `imports` of classes from different packages that this class may need to reference
* This class `access modifer`, keyward `class` followed by the class name.
* Class and method bodies are enclosed with `{}`
* Uninitialized primitives are defaulted to 0, boolean to false.
* Uninitialized object references are defaulted to null.

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
* The `new` operator creates an Object, allocating memory to store this object
* You may assign an object reference to a variable of the appropriate type.
* Access variable or methods of the object using `.` operator.

#### Local Variables and Recursive Object Reference

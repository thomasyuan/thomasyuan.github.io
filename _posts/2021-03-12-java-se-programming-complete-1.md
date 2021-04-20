---
title: "Java SE: Programming Complete - 1"
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

## Introduce to Java 

#### How Java Works
* Source code is plain text `.java`
* Compiler compiles the source code to byte-code `.class`
* JVM run your application by translating the byte-code to platform-specific code

#### Class and Object
* Java code is structured with class
* Class represent a concept or a type of thing
* Object is a specific instance of class

#### Access Modifier
* public: visible to any class
* protected: visible to same package or sub-class
* default: visible to same package only
* private: visible only within same Class

#### Application Entry Point
* main method
* must be public
* must be static
* must be void
* must accept array of String object as the parameter

`public static void main(String[] args)`

#### Compile
* compile with `javac`
* `-classpath` or `-cp` points to the location of other classes might be used to compile you source code
* `-d` points to the path of the compilation result
* the source code
`javac -classpath /project/classes -d /project/classes /project/source/ca/learnprogramming/Test.java` 

#### Run
* `-classpath` or `-cp` points to the location where your classes are located
* full qulified class name
`java -classpath /project/classes ca.learnprogramming.Test`
> Start from Java 11, you can also just run `java single-file-java-source-code`.

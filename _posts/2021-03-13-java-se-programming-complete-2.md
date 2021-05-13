---
title: "Java SE: Programming Complete - 2"
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

## Primitive Types, Operators, and Flow Control Statements

#### Whole Numbers

- byte - 8 bits (1 byte)
- short - 16 bits (2 bytes)
- int - 32 bits (4 bytes)
- long - 64 bits (8 bytes)
  > Default value is 0 or 0L

#### Floating point numbers

- float - 32 bits (4 bytes)
- double - 64 bits (8 bytes)
  > Default value is 0.0 or 0.0F

#### Boolean

- boolean - true of false
  > Default value is false

#### Character

- char - 16 bits (0 - 65535)
  > default value '`\u0000`' (`\u` means unicode)

#### Arithmetic Operations and Type Casting

- Smaller types are automatically casted to bigger types
  > byte->short->char->int->long->float->double
- A bigger type value can't be assigned to a smaller type variable without explicit type casting, beware of a possible overflow
- **Resulting type of arithmetic operations on types smaller than int is an int; otherwise, the result is of a type of a largest participant.** (not apply to `++` or `--`, which means short++ will still be a short)

#### Bitwise Operators

- Signed Left Shift `<<` shifts each bit to the left by specified number of positions, fills low-order positions with 0 bit values.
- Sighned Right Shift `>>` shifts each bit to the right by specified number of positions.
- Unsigned Right Shift `>>>` same as above, but fills high-order positions with 0 bit values.

#### Flow Control Using `switch` Construct

- Switch expression must be of one of the following types: `byte`, `short`, `int`, `char`, `String`, `enum`
- If the switch expression did not match any of the cases, then the `default` case is executed. It doesn't not have to be the last case in the sequence and it's optional.

#### JShell

JShell was introduced in JDK 9 as part of Java Enhancement Proposal (JEP) 222 under project Kulla. Many programming languages, such as JavaScript, Python, Ruby, etc., provide easy-to-use, command-line tools for their execution, but Java was still missing such a utility. So, JDK 9 introduced the Java shell (JShell) tool.

> https://developers.redhat.com/blog/2019/04/05/10-things-developers-need-to-know-about-jshell/

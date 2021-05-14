---
title: "Java SE: Programming Complete - 8"
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

## Arrays and Loops

#### Arrays

- An array is a fixed-length collection of elements of the same type indexed by int
- Declare array: `int[] primes;` or `int primes[]`
- Create array: `primes = new int[4]`
  - Once an array is created, its length can't be changed.
  - An array of object reference is filled with `null` values
  - An array of primitive values is filled with 0 values (or `false` for `boolean`)
- Combined Declaration and Creation `int[] primes = new int[3]`
- Combined create of the array object and initialization of the array content:

```java
int[] primes;
primes = new int[]{1, 2, 3};
```

- Combined declaration and creation of the array object as well as the initialization fo the array content: `Product[] products = {new Product("Cake"), new Product("Tea"), new Product("Beer")};`

#### Multidimensional Arrays

- Can be of non-square shapes `int[][] matrix = { {4, 1}, {2, 0, 5} };`
- Can have more than two dimensions

#### Copying Array Content

- Java arrays are of fixed length (can't be resized)
- However, resize can be emulated by creating a new array with a different size and copying all or partial content from the original array to the new array object, using `System.arrayCopy(<source array>, <source position>, <dest array>, <dest position>, <length>)` or `<new array> = Arrays.copyOf(<source array>, <new array length>)` or `<new array> = Arrays.copyOfRange(<source array>, <start position>, <end position>)`

#### Arrays Class

- The `java.util.Arrays` class provides convenience methods for handling arrays, such as:
  - Filling array with values `Arrays.fill`
  - Searching through the array `Arrays.binarySearch`
  - Comparing content `Arrays.equals`
  - Sorting array content using `Comparable` or `Comparator`

#### Break and Continue

- You can give a loop with a label.
- `break` terminates the current loop.
- `break <label>` terminates the labeled loop.
- `continue` operator skips the current loop cycle.
- `continue <label>` skips the labeled loop cycle.

```java
char[][] matrix = {{'A', 'B', 'C', 'D', 'E'},
                   {'F', 'G', 'H', 'I', 'K'},
                   {'L', 'M', 'N', 'O', 'P'},
                   {'Q', 'R', 'S', 'T', 'U'},
                   {'V', 'W', 'X', 'Y', 'Z'}};
StringBuilder txt = new StringBuilder();
outerLoopLabel:
for (char[] row : matrix) {
  for (char value: row) {
    if (value == 'C') { continue; }
    if (value == 'H') { continue outerLoopLabel; }
    if (value == 'N') { break; }
    if (value == 'S') { break outerLoopLabel; }
    txt.append(value);
  }
  txt.append('\n');
}
```

The output of this code is `ABDE\nFGLM\nQR`;

---
title: "Java Unit Test: JUnit5"
excerpt_separator: "<!--more-->"
toc: true
categories:
  - Blog
tags:
  - Java
  - Unit Test
---


> Source 
> * [JUnit5 Basics](https://www.youtube.com/playlist?list=PLqq-6Pq4lTTa4ad5JISViSb2FVG8Vwa4o) 
> * [JUnit 4 & 5 Annotations](https://medium.com/@rhamedy/junit-annotations-every-developer-should-know-eb972a7a26c9)
> * 

## Lifecycle/Hook Points
For JUnit5, it's `@BeforeAll` `@AfterAll` and `@BeforeEach` and `@AfterEach`. (For JUnit4, it's `@BeforeClass` `@AfterClass` and `@Before` `@After`)

@BeforeAll will be excueted before the test class instance being created, so generally it should be static method. Unless you 
change the TestInstanc lifecycle from PER_METHOD to PER_CLASS by `@TestInstance(TestInstance.lifecycle.PER_CLASS)`.


## Annotations
### @Test
If you only use one annotation, then it must be `@Test`. `@Test` tells JUnit that the function a test funciton.

### @BeforeEach/@AfterEach
Before/After every `@Test` method gets called. it could be used to setup/teardown the test.

### @DisplayName
Give the test function a readable output, not class/function name. for example `@DisplayName("Test Suite for Class A")`.

### @Disabled
Skip running a test. (JUnit4 it's `@Ignore`)

### @RepeatedTest
Run the test several times, for example `@RepeatedTest(5)` will run the test 5 times.

### @Nested
You can use `@Nested` to group some tests in a test class.

### Conditional Excution
* `@EnabledOnOs(OS.LINUX)` / `@DisabledOnOs(OS.MAC)`
* `@EnabledOnJre(JRE.JAVA_11)` / `@DisabledOnJre(JRE.JAVA_11)`
* `@EnabledIf`
* `@EnabledIfSystemProperty`
* `@EnabledIfEnvironmentVariable`


## Assertion
There are many assertions like `assertEqules`, `assertTrue` etc. 
In JUnit4, `@Test` could have parameters, but in JUnit5, all `@Test` paramters are move to Assertions.
For example, `@Test(expected = Exception.class)` changes to `assertThrows(Exception.class, () -> {...});`
`@Test(timeout = 10)` will change to `assertTimeout(Duration.ofMillis(10), () -> Thread.sleep(100));`



## Assumption
Like assertions, there are many assumptions as well, if the assumption is not matched, then the
test will be skipped.


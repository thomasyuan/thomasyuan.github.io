---
title: "Output Gradle Test Result to Console"
excerpt_separator: "<!--more-->"
toc: true
categories:
  - Blog
tags:
  - Gradle
---

> Source https://stackoverflow.com/questions/3963708/gradle-how-to-display-test-results-in-the-console-in-real-time

The `gradle test` output doesn't make any sense. Here is the way to fix it.

## Use Test Logging Event

```
test {
    testLogging {
        // optional, when you need run all tests even the code is not changed.
        outputs.upToDateWhen {false}
        // If use junit 5, need enable JUnit Platform support
        useJUnitPlatform()
        events "passed", "skipped", "failed"
    }
}
```

For android project, it will be something like this:

```
android {
    ...
    testOptions {
        unitTests.all {
            testLogging {
                outputs.upToDateWhen {false}
               // If use junit 5, need enable JUnit Platform support
                useJUnitPlatform()
                events "passed", "skipped", "failed"
            }
        }
    }
    ...
}
```

## Use com.adarshr.test-logger plugin

```
plugins {
    id 'com.adarshr.test-logger' version '<version>'
}
```

Reference here https://plugins.gradle.org/plugin/com.adarshr.test-logger

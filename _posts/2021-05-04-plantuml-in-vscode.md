---
title: "PlantUML in VS Code"
excerpt_separator: "<!--more-->"
toc: true
categories:
  - Blog
tags:
  - UML
  - VSCode
---

## Test

```java
#@startuml

class ExampleClass {
    -mPrivate: String
    +mPublic : int
    #mProtected: boolean
    ~mDefault: float
    mNothing: long
    +void publicMethod(int)
    -boolean privateMethod(String)
    ~String defaultMethod(boolean)
    #int protectedMethod()
}

class DerivedClass {
    +oneMoreMethod()
}

interface Fly {
    +fly()
}

interface Runnable {
    +run()
}

ExampleClass <|-- DerivedClass
Fly <|.. DerivedClass
ExampleClass *-- Runnable

#@enduml
```

Output
{% include figure image_path="/assets/diagram/2021-05-04-plantuml-in-vscode-1.png" alt="68-95-99.7 rules" %}

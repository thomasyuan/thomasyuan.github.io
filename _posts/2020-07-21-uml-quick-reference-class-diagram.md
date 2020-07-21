---
title: "UML quick reference - Class Diagram"
excerpt_separator: "<!--more-->"
categories:
  - Blog
tags:
  - UML
  - Note
---

> Source https://www.visual-paradigm.com/guide/uml-unified-modeling-language/uml-class-diagram-tutorial/, Reference http://ifeve.com/uml-intro/

## Class Diagram

### Class Notation
1. Class Name
2. Class Attributes
3. Class Operations (Method)


 
#### Visibility
* \+ denotes public attributes or operations
* \- denotes private attributes or operations
* \# denotes protected attributes or operations
* ~ denotes default (package only) attributes or operations

### Parameter Directionality
* in
* inout
* out

### Perspectives of Class Diagram
* **Conceptual**: represents the concepts in the domain
* **Specification**: focus is on the interfaces of Abstract Data Type (ADTs) in the software
* **Implementation**: describes how classes will implement their interfaces

## Relationships between classes
* Generalization (Inheritance): Represents an "is-a" relationship.
* Realization: (Interface implemention) the reationship between blueprint and implemention
* Association: two classes have relationship
* Dependency: A special type of association, class is used in parameter but not stored as a member varible.
* Aggregation: A special type of association, represents a "part of" relationship. Two classes have separate lifetimes.
* Composition: A special type of aggregation where parts are destroyed when the whole is destroyed. (same lifetime)

![relationship symbols](assets/images/blogs/uml_classes_relationship.png)

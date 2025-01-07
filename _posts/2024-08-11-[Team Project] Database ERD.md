---
title:  "[Team Project] Database ERD"
categories: [backend,java,project]
tags:
  [
    notion,
    figma,
    java,
    spring,
    ERD
  ] 
---
# DataBase E-R Diagram
![ERD Diagram](/assets/img/erd.png)

## Dependency Management
### Referential Integrity (참조 무결성)
* Make sure the parent table and child table are 8correctly linked using a foreign key.
* Design the database so that data stays consistent if something is deleted or updated.

### Avoid Circular Dependencies (순환 참조 방지)
* Avoid situations where two or more tables depend on each other in a loop.
* Circular dependencies can cause problems when deleting or updating data.
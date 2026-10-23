---
title: "체육시설 예약 팀 프로젝트 - ERD 설계"
categories: [Project, Gym Booking]
tags: [team-project, database, erd]
redirect_from:
  - "/posts/Team-Project-Database-ERD/"
---
# DataBase E-R Diagram
![ERD Diagram](/assets/img/posts/2024-08-11-gym-booking-erd/01-erd.png)

## Dependency Management
### Referential Integrity (참조 무결성)
* Make sure the parent table and child table are 8correctly linked using a foreign key.
* Design the database so that data stays consistent if something is deleted or updated.

### Avoid Circular Dependencies (순환 참조 방지)
* Avoid situations where two or more tables depend on each other in a loop.
* Circular dependencies can cause problems when deleting or updating data.
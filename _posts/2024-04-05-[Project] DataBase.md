---
title:  "[CRUD Practice] Project - DataBase"
categories: [Project, Personal]
tags:
  [
    DB
  ] 
---

## Database

DBMS : mariaDB

I will use single schema

> schema : market

### Table

> items : 게시글
>
> member : 회원정보
>
> > ### Items
> >
> > Primary key : post_id
> >
> > | post_id | post_name | member |     date     | price |
> > | :-----: | :-------: | :----: | :----------: | :---: |
> > |    1    |   desk    |  명진  | 24/4/1 13:15 | 5,000 |
> > |    2    |           |  명선  |              |       |
> > |    3    |           | 복돌이 |              |       |
>
> >
> >
> >### Member
> >
> >primary key : member_id
> >
> >| member_id |     name      | password |
> >| :-------: | :-----------: | :------: |
> >|     1     | unique = true |          |
> >|     2     |   char(10)    | char(20) |
> >
> >

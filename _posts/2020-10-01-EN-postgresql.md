---
title: "[에러노트] database 'template1' is being accessed by other users. DETAIL: There are 1 other session(s) using the database."
excerpt: "postgreSQL에서 'template1' is being accessed by other users. DETAIL: There are 1 other session(s) using the database 에러시 해결법"
categories:
- ErrorNote
tags:
- error
- postgreSQL
- database
toc: true
toc_sticky: true
toc_label: 목차
---

참고 : [https://www.python2.net/questions-288205.htm](https://www.python2.net/questions-288205.htm)

## 해결 방법

template1에 연결된 데이터베이스 세션을 닫아야 한다.

→ 셸 열어서 명령어 입력

```sql
postgres=# select pg_terminate_backend(pid)
postgres-# from pg_stat_activity
postgres-# where datname = 'template1';
 pg_terminate_backend
----------------------
 t
(1개 행)
```

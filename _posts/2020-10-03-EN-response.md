---
title: "[에러노트] UT005023: Exception handling request to [Path]: java.lang.IllegalStateException: UT010019: Response already commited"
excerpt: "java.lang.IllegalStateException: UT010019: Response already commited 에러시 해결법"
categories:
- ErrorNote
tags:
- error
- java
toc: true
toc_sticky: true
toc_label: 목차
---

ERROR [io.undertow.request] (default task-1) UT005023: Exception handling request to [Path]: java.lang.IllegalStateException: UT010019: Response already commited

찾아냈다...  포워딩의 문제였다.

### 해결방법

- 나의 경우 Ajax로 되돌려주어야 하는 데이터를 자바에서 forward 객체를 사용하여 포워딩을 했다. 이걸 프론트 컨트롤러에서 dispatcher를 사용하여 포워딩을 시키는 거였는데 에러가 난 거.
- 자바에서 return forward; 부분을 return null로 바꿈. → 해결
- Response already commited 이게 힌트였을까.. 이미 응답이 왔는데 또 보냈다,, 뭐 그런걸까,,

### 함께 보면 좋을 자료

- [dispatcher와 redirect의 차이](https://devbox.tistory.com/entry/Comporison-Dispatcher%EB%B0%A9%EC%8B%9D%EA%B3%BC-Redirect-%EB%B0%A9%EC%8B%9D)

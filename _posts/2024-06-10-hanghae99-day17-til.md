---
title: "[항해99 취업 리부트 코스 학습일지][day17] 시간 분배의 싸움"
excerpt: ""
categories:
  - TIL
tags:
  - 개발자포트폴리오
  - 개발자이력서
  - 개발자취업
  - 개발자취준
  - 코딩테스트
  - 항해99
  - 취리코
  - 취업리부트코스
toc: true
toc_sticky: true
toc_label: "목차"
toc_icon: "edit"
# classes: wide
header:
  teaser: /assets/images/hanghae99-teaser.png
---
## 📍TIL

### 핵심 키워드
- DFS, BFS

### 새로 배운 내용
#### 파이썬의 global 키워드 언제 쓰지?
- [참고1](https://lets-hci-la-ai-withme.tistory.com/68), [참고2](https://www.w3schools.com/python/python_variables_global.asp)
- 함수 내부에서 생성한 변수는 **로컬변수**이지만 `global` 키워드를 사용하면 함수 내부의 변수를 **전역**으로 사용할 수 있다.
- 또한 **전역변수 값**을 함수 **내부에서 바꿀 때**에도 `global` 키워드를 사용하여 참조할 수 있다.

#### 더 깊은 재귀 호출에 사용하는 `sys.setrecursionlimit`
- 파이썬은 재귀 함수 최대 깊이에 제한이 있다. (maximum recursion depth)
	- 1000 이상 호출시 `RecursionError` 발생함
- BOJ 채점 서버에서는 이 값이 1,000으로 되어있다. ([참고](https://help.acmicpc.net/judge/rte/RecursionError))
```python
from sys import setrecursionlimit
setrecursionlimit(10 ** 6)
```

### 트러블슈팅 or 고민한 내용
- 초기화를 잘못해서 계속 틀리기도 하고 템플릿에서 살짝 변형이 되니 도저히 풀 수가 없기도 했다. 휴 어쩌지


### 생각
- 알고리즘이 갈수록 어려워지니 여기에 투입되는 시간이 자동으로 많아지는데,, 기술 공부 어쩌냐


### 🥰 오늘의 잘한 일
- 템플릿 외우려고 계속 반복했다.
- 어려워도 일단 시도한 점..?

### 💪 오늘의 아쉬운 일 & Action Plan
- 아직까진 활용이 후루룩 되진 않는다

<br>
<br>
<br>

<p>
  <p style="color:grey">항해99 취업 리부트 코스를 수강하고 작성한 콘텐츠 입니다.</p>
  <a href="https://hanghae99.spartacodingclub.kr/reboot" target="_blank" class="img-link">
    <img src="https://github.com/grey920/grey920.github.io/assets/58028215/84b7ba76-a278-4b8c-a8af-0b0ca7da095b" alt="항해99 - 온라인 코딩 부트캠프 항해99" loading="lazy">
  </a>
</p>
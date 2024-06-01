---
title: "[항해99 취업 리부트 코스 학습일지][day10] 알고리즘 유니온!"
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

## 📍오늘의 목표
- [x] 추가 문제 하나 더 풀기

## 📍TIL
### 핵심 키워드
- CIDR

### 새로 배운 내용
#### 핵심만 읽고 문제 풀기
1. solution() 함수 만들고 시작
	```python
	def solution():
		return
	print(solution())
	```
2. 문제에서 `예시` 복사해서 상단에 주석으로 붙임
3. 문제의 예제 입력을 코드에 넣고 함수의 파라미터로 받기 
	```python
	def solution(string: str):
		print(string)
		return
	string = '입력예시1'
	string = '입력예시2'
	string = '입력예시3'
	print(solution(string))
	```
4. 함수 안에서 print로 찍어보며 로직 작성
5. print문 제거하고 리팩토링

#### 진법 변환
- b진수 ➡️ 10진수로 변환할 때는 `int(string, base)` 내장 함수 사용
	- 내장 함수인 int()를 사용하면 C언어로 구현해서 최적화되어 직접 코드를 구현하는 것보다 효율적이다.
	- 내장 함수는 메모리 사용도 최적화하도록 설계되어 있어서 대규모 데이터 처리시에도 메모리 오버헤드를 최소화하는 데 도움이 된다.
	- 이미 오랜 기간동안 사용해서 검증된 코드기 때문에 버그도 적고, 안정적으로 동작한다.
#### 직접 구현보다 효율적인 함수들 (한 번 더 체크하기!)
##### 1. sorted() 함수

##### 2. sum() 함수

##### 3. min() / max() 함수

##### 4. map() 함수

##### 5. len() 함수


#### 입력값 여러 줄 받기


#### 리스트내에 다른 리스트의 요소 있으면 제거하기 ➡️ 차집합 사용


#### 문자열 바꾸는 replace()와 translate()


### 트러블슈팅 or 고민한 내용


### 생각
- 기술 매니저님이 데브옵스 멘토링이 있으셔서 6시로 팀 스터디를 하셨다. 와.. 7년차가 되어도 저렇게 열심히 배우고 나누고 하시는데.. 나는 진짜 더 열심히 해야겠다.

### 🥰 오늘의 잘한 일
- 5문제 제출 목표를 이루어냈다..ㅎ 다음주엔 6개 풀어보자~~
- 잘한 일이라기 보단, 좋았던 일
	- 알고리즘 9조와 10조가 처음 함께 모여서 팀 스터디를 받은 날! 기술 매니저님이 오시기 전에 함께 모여서 문제를 어떻게 풀었는지 설명도 듣고 서로의 코드도 보면서 많이 배울 수 있었다. 아직까진 매우 만족!

### 💪 오늘의 아쉬운 일 & Action Plan
- 새로 알게된 내용을 좀 더 깊게 알아보고 정리해서 적어두고 싶은데 체력이 달려서 자꾸만 엎어지게 된다..
  ➡️ 영양제!!! 그리고 점심에 산책 꼭 가기!

<br>
<br>
<br>

<p>
  <p style="color:grey">항해99 취업 리부트 코스를 수강하고 작성한 콘텐츠 입니다.</p>
  <a href="https://hanghae99.spartacodingclub.kr/reboot" target="_blank" class="img-link">
    <img src="https://github.com/grey920/grey920.github.io/assets/58028215/84b7ba76-a278-4b8c-a8af-0b0ca7da095b" alt="항해99 - 온라인 코딩 부트캠프 항해99" loading="lazy">
  </a>
</p>
---
title: "[알고리즘] Quick 퀵정렬"
excerpt: 퀵 설명 (분할 정복 알고리즘)
categories:
- Algorithm
tags:
- Summary
- Sort
last_modified_at: 2020-08-29T11:48:00-05:00
---

# 퀵 정렬??

### 특정한 값을 기준으로 큰 숫자와 작은 숫자를 서로 교환한 뒤에 배열을 반으로 나눈다. → 왼쪽값과 *피벗값을 교환한다

*피벗값(pivot) : 중심축, 기준값. 피벗을 기준으로 피벗보다 작은 값은 왼쪽으로, 피벗보다 큰 값은 오른쪽으로 셋팅한다.

## 퀵정렬의 분할 정복 과정

- 분할 : 정렬할 자료들을 기준값을 중심으로 2개의 부분집합으로 분할
- 정복 : 기준보다 작은 값은 왼쪽, 기준보다 큰 값은 오른쪽 부분집합으로 정렬. 부분집합의 크기가 1이하가 아니면 순환 호출을 이용해 다시 분할.

[출처] : [https://heekim0719.tistory.com/282](https://heekim0719.tistory.com/282) 

## 퀵 정렬의 방법

1. 피벗을 중심으로 L과 R값을 지정해준다. L은 피벗보다 큰 값, R은 피벗보다 작은 값을 지정.
2. 두 개 모두 선택되었다면 자리를 교환한다
3. 만약 한 쪽이 선택된 L이나 R이 없다면 선택된 값과 피벗값을 교환한다.

## 평균 시간복잡도는 `O(N*log(2)N)`

다른 정렬 방법에 비해 뛰어난 실행 시간 성능을 가지고 있다.   

하지만, 이미 정렬된 상태의 데이터라면 최악의 성능을 갖게 된다(N^2) 

예) 최악의 경우

[https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbZMbC4%2FbtqCSft0mnb%2FAFz9gc2HDMt37INjvlFWok%2Fimg.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbZMbC4%2FbtqCSft0mnb%2FAFz9gc2HDMt37INjvlFWok%2Fimg.png)

- 피벗을 제외한 나머지 모든 원소가 하나의 부분배열로 분할되는 경우 : 즉, 피벗이 항상 부분배열의 최소값 혹은 최대값이 되는 경우
- 입력 데이터가 정렬된 데이터이고 피벗이 배열의 처음 원소인 경우

[https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FUcbiY%2FbtqCVDGXzWI%2FDoo5JH2JN2y3m6qktKjLV0%2Fimg.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FUcbiY%2FbtqCVDGXzWI%2FDoo5JH2JN2y3m6qktKjLV0%2Fimg.png)
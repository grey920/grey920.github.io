---
title: "[알고리즘] Selection 선택정렬"
excerpt: 선택정렬 설명
categories:
- Algorithm
tags:
- Summary
- Sort
last_modified_at: 2020-08-29T11:48:00-05:00
---

# 선택정렬이란??

## "가장 작은 것을 선택해서 제일 앞으로 보낸다"

```java
int[] arr = {1, 10, 5, 8, 7, 4, 6, 3, 2, 9};
int temp;
for(int i=0; i<arr.length-1; i++){ //arr.length-1 : 마지막은 이미 정렬된 상태니까 뺀다
	for(int j=i+1; j<arr.length; j++){ //j=i+1 : i 다음 번호부터 시작한다
		if(arr[i] > arr[j]){
			temp = arr[j];
			arr[j] = arr[i];
			arr[i] = temp;
		}
	}
}
for(int i=0; i<arr.length; i++){
	System.out.print(arr[i]);
}
```

## 데이터가 N개일 때 총 몇 번의 연산을 해야할까?

### 약 N * (N+1) / 2번 ⇒ 빅 오 표기법으로는 `O(N^2)`

> 빅 오 표기법 (big-O natation)

알고리즘의 효율성을 표기해주는 표기법으로 상한선을 기준으로 표기하기 때문에 보통 알고리즘의 시간 복잡도(알고리즘의 시간 효율성)와 공간 복잡도(알고리즘의 메모리 효율성)를 나타내는데 주로 사용된다.

출처([https://noahlogs.tistory.com/27](https://noahlogs.tistory.com/27))
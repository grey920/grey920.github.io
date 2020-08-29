---
title: "[알고리즘] Insert 삽입정렬"
excerpt: 삽입정렬 설명
categories:
- Algorithm
tags:
- Summary
- Sort
last_modified_at: 2020-08-29T11:48:00-05:00
---

# 삽입정렬??

## "각 숫자를 *적절한 위치에 삽입하면 어떨까?"

*적절한 위치: 앞 원소의 자리에서 필요할때에만 위치를 바꾼다 ⇒ (거의 정렬된 상태라면)연산이 적다 ⇒ 효율적이다.

### 🌟 기준의 왼쪽 값들은 모두 정렬이 되었다고 가정한다

```java
int[] arr={1, 10, 5, 8, 7, 4, 6, 3, 2, 9};
int temp;

for(int i=1; i<arr.length; i++){
	for(int j=i; j>0; j--){
		if(arr[j-1] > arr[j]){
			temp = arr[j-1];
			arr[j-1] = arr[j];
			arr[j] = temp;
		}
	}
}
for(int a : arr){
	System.out.print(a);
}
```

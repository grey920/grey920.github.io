---
title: "[알고리즘] Bubble 버블정렬"
excerpt: 버블정렬 설명
categories:
- Algorithm
tags:
- Summary
- Sort
last_modified_at: 2020-08-29T11:48:00-05:00
---

# 버블정렬
> 정렬들 중 가장 직관적이고 가장 비효율적인 알고리즘   
   

   
   
# 버블정렬이란??

### "바로 옆에 있는 값과 비교해서 더 작은 값을 앞으로 보내면 어떨까?"

⇒ 1회 수행시 **가장 큰 값**이 가장 **오른쪽**에 정렬됨

```java
int[] arr = {1, 10, 5, 8, 7, 4, 6, 3, 2, 9};
int temp;

for(int i=0; i<arr.length; i++){
  for(int j=0; j<arr.length-i-1; j++){
    if(arr[j] > arr[j+1]){
        temp = arr[j];
        arr[j] = arr[j+1];
        arr[j+1] = temp;
      }
   }
}
for(int a : arr){
System.out.print(a);
}
```

## 시간복잡도
(n-1) + (n-2) + ... + 2 + 1 => n(n-1) / 2   
즉, `O(N^2)`   
* 버블정렬은 한 번의 순회를 마칠 때마다 비교 대상이 하나씩 줄어들기 때문에 전체 원소의 갯수가 n개라면, 총 n-1번 순회할 때 정렬이 끝난다.

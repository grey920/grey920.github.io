---
title: "[알고리즘] Merge Sort 병합정렬"
excerpt: 병합정렬 설명 - "일단 반으로 나누고 나중에 합쳐서 정렬하면 어떨까?"
categories:
- Algorithm
tags:
- Summary
- Sort
---

# 병합 정렬 (Merge Sort)

자료 출처 : 나동빈님 블로그 ([https://blog.naver.com/ndb796/221227934987](https://blog.naver.com/ndb796/221227934987))

## "일단 반으로 나누고 나중에 합쳐서 정렬하면 어떨까?"

> 배열을 앞 부분과 뒷 부분으로 나누어 각각 정렬한 다음 병합하는 작업을 반복하여 정렬을 수행하는 알고리즘

- 이것도 퀵 정렬처럼 **'분할 정복'** 방법을 채택한 알고리즘. 따라서 **시간복잡도** 역시 `O(N*logN)`이다
- 그러나 퀵 정렬과 달리, 병합 정렬은 정확히 반절씩 나눈다는 점에서 최악의 경우에도 O(NlogN)을 보장한다.


> 합치는 순간에 정렬을 수행한다

합치는 단계는 3단계면 된다. 합치는 갯수는 1→2→4→8로 2배씩 증가. 즉 2^3=8이므로 3단계만 필요하다.

즉, 데이터의 갯수가 N개일 때 정렬 자체에 필요한 수행시간은  N(데이터 갯수만큼) , 높이는 logN(단계의 크기)으로 총 시간복잡도는 **O(N*logN)**이다. 

### 왜 정렬에 필요한 수행시간이 N일까?

- 삽입 정렬과 마찬가지로 '부분 집합은 이미 정렬이 되어있는 상태'라고 **가정**하기 때문!


이미 정렬된 상태의 두 배열을 정렬할 때 비교는 데이터 갯수 N번만큼만 하면 된다.

```java
package sort.merge;

import java.util.Scanner;

// 병합정렬 알고리즘
// 전체 시간 복잡도는 O(n log n)
/* 배열의 요소 개수가 2개 이상인 경우
 	1. 배열의 앞부분을 병합 정렬로 정렬한다
 	2. 배열의 뒷부분을 병합 정렬로 정렬한다
 	3. 배열의 앞부분과 뒷부분을 병합한다
  */
public class MergeSort {
	static int[] buff;	// 작업용 배열
	
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		
		System.out.println("병합 정렬");
		System.out.print("요솟수 : ");
		int nx = sc.nextInt();
		int[] x = new int[nx];
		
		for(int i=0; i < nx; i++) {
			System.out.print("x["+i+"]: ");
			x[i] = sc.nextInt();
		}
		
		mergeSort(x, nx);	// 배열 x를 병합정렬
		
		System.out.println("오름차순으로 정렬했습니다");
		for(int i = 0; i < nx; i++)
			System.out.println("x["+i+"]= "+ x[i]);

		sc.close();
	}

	private static void mergeSort(int[] a, int n) {
		buff = new int[n];		//병합한 결과를 일시적으로 저장할 작업용 배열 생성
		__mergeSort(a, 0, n-1);	//실제로 정렬 작업을 수행할 __mergeSort()메서드를 호출하여 배열 전체를 병합 정렬한다
		buff = null;			// 작업용 배열을 해제
	}

	// a[left] ~ a[right]를 재귀적으로 병합 정렬	// left=0, right:n-1
	private static void __mergeSort(int[] a, int left, int right) {
									//a:정렬할 배열, left/right : 첫번째/마지막 요소의 인덱스
		if(left < right) {
			int i;
			int center = (left + right)/2;
			int p = 0;
			int j = 0;
			int k = left;
			
			
			__mergeSort(a, left, center);	// 배열의 앞부분 정렬
			__mergeSort(a, center+1, right);// 배열의 뒷부분 정렬
			
			// 정렬 후 병합을 수행하는 코드
			for(i=left; i<= center; i++)	// 배열의 앞부분인 a[left]~a[center]을 buff[0]~buff[center-left]에 복사한다
				buff[p++] = a[i];			// for문이 끝날 떄 p의 값은 복사한 요솟수 center-left+1이다
			
			while(i <= right && j < p)		// 배열의 뒷부분인 a[center+1]~a[right]와 buff로 복사한 배열의 앞부분 p개를 병합한 결과를 배열a에 저장한다 
				a[k++] = (buff[j] <= a[i]) ? buff[j++] : a[i++];
				
			while(j < p)
				a[k++] = buff[j++];		// 배열 buff에 남아 있는 요소를 배열 a에 복사한다
		}
	}

}
```

# 병합 정렬을 구현할 때 신경써야 할 부분??

- 위 코드의 buff처럼 정렬에 사용되는 배열은 전역 변수'로 선언되어야 한다.  병합 정렬은 '기존의 데이터를 담을 추가적인 배열 공간이 필요하다'는 점에서 메모리 활용이 **비효율적**이다.

## 병합 정렬은 일반적인 경우 퀵 정렬보다 느리지만 어떠한 상황에서도 정확히 O(NlogN)을 보장할 수 있다는 점에서 몹시 효율적인 알고리즘이다.

---
title: "[자료구조] Linked List"
excerpt: 생활코딩의 DataStructure 강의를 듣고 정리한 Linked List 설명입니다
categories:
- DataStructure
tags:
- List
- LinkedList
toc: true
toc_sticky: true
toc_label: LinkedList
---

# Linked = '연결'

- 연결이 무엇인가
- 링크드 리스트에서 말하는 연결을 프로그래밍적으로 어떻게 표현하는가

# 그 전에 알아야 할 것

## 메모리

기억을 담당. 스토리지에 비해 매우 비싸고 용량이 작다. 전원을 끄면 데이터가 사라진다. 스토리지보다 훨씬 빠르게 데이터를 저장하고 가져온다. 

## CPU

생각, 계산, 연산을 담당. 셋 중 가장 처리 속도가 빠르다. 

## 스토리지 (HDD/SSD)

저장장치. 가격이 저렴하다. 용량이 크고 전원이 꺼져도 데이터가 저장되어 있다. 

**데이터의 흐름 : 스토리지 ⇒ 메모리 ⇒ CPU**

# 데이터 스트럭쳐의 대상은 '메모리'

메모리의 효율적 사용이 데이터 스트럭쳐의 미션이다.

## 건물로 예시를 들자

건물 : 메모리라 할 때,

건물에는 사무실들이 있고 각각의 사무실에는 **호수(address)**가 있다. 

주소가 가리키는 각각의 위치에 데이터가 저장되어 있다!

**메모리의** 중요한 특징 : 각각의 주소에 접근할 때 걸리는 시간이 동일하다. 

"Random Access Memory" (RAM)

### 즉, Address를 알고 있다면, 아주 빠르게 데이터를 가져올 수 있다!

[메모리를 사용하는 방식에서의 차이]

- Array List - 같은 엘리먼트들이 연속적으로 붙어있다.
- Linked List - 각각의 데이터들이 흩어져 있고 서로 연결되어 있다.

# Linked List의 구조

엘리먼트 == node, vertex 

프로그래밍에서 노드 : 객체를 이용해서 노드를 표현 

- 노드의 두 가지 변수(필드)
    1. 실제 값(Data field)
    2. 다음 노드에 대한 것 (Link field)

## 링크드리스트를 이용하려면 '첫번째 노드'가 무엇인가를 알아야 한다!

그래야 그를 통해 두번째 노드를 찾고, 세번째 노드를 찾고,, 찾는다.

첫번째 노드에 대한 정보를 **HEAD필드**에 적는다. 

# 데이터 추가

```java
Vertex temp = new Vertex(input) // input에 새로운 노드 값을 넣는다
temp.next = head // temp의 다음 값으로 현재 첫번째 노드인 head를 가리킨다
head = temp // head를 새로운 노드인 temp값으로 갱신한다
```

# 중간에 추가하기

예) 15 → 6 → 23 → 4 → 7 → 71

2번 인덱스에 90을 추가한다

```java
Vertex temp1 = head // temp1은 15인 상태
while (--k != 0)  // 1 != 0 (true)
	temp1 = temp1.next  // temp1 = 6
Vertex temp2 = temp1.next // temp2 = 23
Vertex newVertex = new Vertex(input) // 새로운 노드 생성
temp1.next = newVertex // temp1이 새로운 노드를 가리킨다
newVertex.next = temp2
```

- 추가하고자 하는 엘리먼트의 **앞뒤**로 존재하는 엘리먼트의 레퍼런스값을 찾아서, 앞에 것에 temp1, 뒤에 것에 temp2 변수에 담는다!

1. head를 통해서 첫번재 노드를 temp1 변수에 담는다
    - Vertex temp1 = head
2. 현재 k=2 ⇒ —k로 인해 k는 1이 됨 
3. k=1 ⇒ —k로 인해 k는 0이 됨 ⇒ while 실행안함
4. 새로운 노드 생성
5. temp1이 새 노드를 가리키게 만든다
6. 새 노드가 temp2를 가리키게 한다

추가 또는 삭제를 할 때는 서로 가리키고 있는 관계만 바꿔주면 되기 때문에 Linked List는 매우 빠르게 처리된다.

# 데이터 삭제

예) 15 → 6 → 90 → 23 → 4 → 7 → 71

2번째 인덱스 값을 삭제하라

```java
Vertex cur = head // current는 head로 지정(head, cur는 15)
while(--k != 0) // 현재 k는 2 -> --k로 인해 1이 됨.
	cur = cur.next // cur는 6
Vertex tobedeleted = cur.next // 6 다음 수(90)를 tobedeleted 변수(삭제하고자 하는 노드)에 담는다. (90이 23을 알려주기 전까진 90을 삭제하면 안된다)
cur.next = cur.next.next // cur는 6, 그 다음수를 90이 아닌 23으로 만든다(6과 90 모두 23을 가리키고 있는 상태) 
delete tobedeleted
```

1. 첫번째 노드 선택하고 next
2. 넘어가고 삭제할 노드를 선택한다. (90)
3. 삭제하기 전에, 6이라는 노드의 next로 90 다음인 23을 지정한다
4. 90을 삭제한다

# Array List VS Linked List

- Array List는 추가/삭제가 느리고, 인덱스 조회가 빠르다. 배열을 내부적으로 사용하기에 크기에 융통성이 없다.
    - 조회 : random access가 가능하기 때문에 조회가 빠름
    - 추가/삭제 : 빈자리를 만들고 옆으로 하나씩 다 이동시켜야 하기 때문에 느림
- Linked List는 추가/삭제가 빠르고, 인덱스 조회가 느리다. 포인터(참조값)으로 노드가 연결되어 있기 때문에 메모리가 허용하는 한 노드를 무한대로 늘릴 수 있다.
    - 조회 :  순차적으로 이동해야 하기 때문에 조회가 느림
    - 추가/삭제 : 앞뒤에 있는 엘리먼트들의 next 값만 바꿔주면 되기 때문에 빠름
    
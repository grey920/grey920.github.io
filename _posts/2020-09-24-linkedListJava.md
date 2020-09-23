---
title: "[자료구조] LinkeList 자바로 구현하기"
excerpt: 생활코딩 강의 정리 - Linked List를 java로 구현한다
categories:
- DataStructure
tags:
- LinkedList
- java
- 자료구조
toc: true
toc_sticky: true
toc_label: LinkedList 자바로 구현하기
---

# 용어 설명

- HEAD - Linked List에서 누가 첫번째 노드인가를 알려줌
- TAIL - 제일 끝 노드는 누구인지 알려줌 (유지 할수도, 안할수도 있음)
- SIZE - 현재 몇 개의 엘리먼트가 리스트에 있는가
- Data field - 값
- Link field - 다음 리스트에 대한 레퍼런스값을 가진 변수
- node / vertex / element - 객체

# 1. 객체 생성

## LinkedList 클래스와 Main 클래스 생성

LinkedList를 만들 클래스와 실행 클래스를 생성한다.

Main.java

```java
package list.linkedlist.implementation;

public class Main {

	public static void main(String[] args) {
		LinkedList numbers = new LinkedList(); //링크드 리스트 인스턴스화
	}

}
```

LinkedList.java

```java
package list.linkedlist.implementation;

public class LinkedList {
	private Node head;// 누가 첫번재 노드인가
	private Node tail;// 누가 마지막 노드인가
	private int size = 0;
	private class Node{ // 내부 객체 정의 (노드)
		//1. 데이터 저장 //2. 다음이 누구인지 알려줌
		private Object data; // 노드가 저장할 데이터
		private Node next; // 다음 노드에 대한 정보
		// 초기화
		public Node(Object input) {//input : 노드의 값
			this.data = input;
			this.next = null; // 객체 생성시엔 다음이 누군지 모름
		}
		public String toString() {
			return String.valueOf(this.data);
		}
	}
}
```

# 2. 데이터 추가 - addFirst

1. addFirst메소드를 생성

Main.java

```java
public static void main(String[] args) {
		LinkedList numbers = new LinkedList(); //링크드 리스트 인스턴스화
		numbers.addFirst(30);
		numbers.addFirst(20);
		numbers.addFirst(10);
	}
```

2. addFirst()메소드 구현하기

LinkedList.java

```java
public void addFirst(Object input) {
		Node newNode = new Node(input); // data = 30, next = null
		newNode.next = head;
		head = newNode; // LinkedList에서 내부적으로 유지하고 있는 멤버변수 head에 새로 만든 newNode를 지정
		size++; // 0 -> 1
		if(head.next == null) { // 다음 노드가 존재하지 않는다 == 혼자 있다
			tail = head; // 노드가 하나라면, head가 곧 tail이다
		}
	}
```

- Node를 생성하는 메소드 - 새로 만든 노드를 가장 첫번째 노드를 가리키는 head에 값을 넣는다

[LinkedList.java](http://linkedlist.java) 전체코드

```java
package list.linkedlist.implementation;

public class LinkedList {
	private Node head;// 누가 첫번재 노드인가
	private Node tail;// 누가 마지막 노드인가
	private int size = 0;
	private class Node{ // 내부 객체 정의 (노드)
		//1. 데이터 저장 //2. 다음이 누구인지 알려줌
		private Object data; // 노드가 저장할 데이터
		private Node next; // 다음 노드에 대한 정보
		// 초기화
		public Node(Object input) {//input : 노드의 값
			this.data = input;
			this.next = null; // 객체 생성시엔 다음이 누군지 모름
		}
		public String toString() {
			return String.valueOf(this.data);
		}
	}
	public void addFirst(Object input) {
		Node newNode = new Node(input); // data = 30, next = null
		newNode.next = head;
		head = newNode; // LinkedList에서 내부적으로 유지하고 있는 멤버변수 head에 새로 만든 newNode를 지정
		size++;
		if(head.next == null) { // 다음 노드가 존재하지 않는다 == 혼자 있다
			tail = head;
		}
	}
}
```

# 3. 데이터 추가 - addLast

main.java

```java
public static void main(String[] args) {
		LinkedList numbers = new LinkedList(); //링크드 리스트 인스턴스화
		numbers.addLast(10);
		numbers.addLast(20);
		numbers.addLast(30);
	}
```

LinkedList.java

```java
public void addFirst(Object input) {
		Node newNode = new Node(input); // data = 30, next = null
		newNode.next = head;
		head = newNode; // LinkedList에서 내부적으로 유지하고 있는 멤버변수 head에 새로 만든 newNode를 지정
		size++;
		if(head.next == null) { // 다음 노드가 존재하지 않는다 == 혼자 있다
			tail = head;
		}
	}
	
	public void addLast(Object input) {
		Node newNode = new Node(input);
		if(size == 0) { // 만약 데이터가 없다면
			addFirst(input); //데이터를 앞쪽에 넣든 뒤에 넣든 상관 없다
		}else { //데이터가 이미 존재한다면
			tail.next = newNode;
			tail = newNode;
			size++;
		}
	}
```

# 4. Node

내부적으로 사용할 Node 메서드를 만든다.

```java
public Node node(int index) {//Node 인스턴스를 리턴
		
	}
```

메인메소드에서 System.out.println(numbers.node(0));를 실행하면 10을 가지고 있는 노드 객체가 리턴된다.

- 어떤 엘리먼트를 가져오고 싶다면? ⇒ 그 리스트의 첫번째 리스트(노드)를 찾아가야 한다. → 헤드

main.java

```java
public static void main(String[] args) {
		LinkedList numbers = new LinkedList(); //링크드 리스트 인스턴스화
		numbers.addLast(10);
		numbers.addLast(20);
		numbers.addLast(30);
		System.out.println(numbers.node(2));
	}
```

만약 2번 인덱스의 노드값을 구하고 싶다면? 

LinkedList.java

```java
public Node node(int index) {//Node 인스턴스를 리턴
		Node x = head;
		x = x.next;
		x = x.next;
		return x;
	}
```

x = x.next; ← 이 부분이 index만큼 반복한다는 것을 볼 수 있다. 

```java
public Node node(int index) {//Node 인스턴스를 리턴
		Node x = head;
		for(int i=0; i < index; i++) {
			x = x.next;
		}
		return x;
	}
```

- 리턴값 자체가 Node이기 때문에 내부적으로 사용하고 있는 Node객체를 직접 리턴하면 안된다(내부적으로 쓰이는 부품이 외부에 노출되면 안된다)

⇒ public 없애기

# 5. 특정한 위치에 원하는 값 끼워넣기 - add

1번 인덱스 위치에 15값을 넣는 add(1, 15)메소드 생성

main.java

```java
public static void main(String[] args) {
		LinkedList numbers = new LinkedList(); //링크드 리스트 인스턴스화
		numbers.addLast(10);
		numbers.addLast(20);
		numbers.addLast(30);
		numbers.add(1, 15); // index 1의 위치(10과 20 사이)에 15를 넣겠다.
	}
```
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

<br><br>

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

<br><br>

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

<br><br>

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

<br><br>

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

<br><br>

# 5. 특정한 위치에 원하는 값 끼워넣기 - add

1번 인덱스 위치에 15값을 넣는 add(1, 15)메소드 생성 ⇒ 20이 뒤로 밀리고, 10과 20 사이에 15가 들어간다

main.java

```java
public static void main(String[] args) {
		LinkedList numbers = new LinkedList(); //링크드 리스트 인스턴스화
		numbers.addLast(10);
		numbers.addLast(20);
		numbers.addLast(30);
		numbers.add(2, 25); // index 2의 위치(20과 30 사이)에 25를 넣겠다.
	}
```

LinkedList.java

```java
public void add(int k, Object input) { // k : 추가하려는 노드의 리스트 상에서의 인덱스값
		if(k == 0) {
			addFirst(input); //첫번째 위치로 들어온다
		} else { 
			Node temp1 = node(k-1);
			Node temp2 = temp1.next;
			Node newNode = new Node(input); // 새로운 노드 생성
			temp1.next = newNode;
			newNode.next = temp2;
			size++;
			if(newNode.next == null) {
				tail = newNode;
			}
		}
		
	}
```

<br><br>

# 6. 확인하기 - toString

```java
System.out.println(numbers);
```

⇒ 결과값 : list.linkedlist.implementation.LinkedList@28a418fc

### 잘 알아볼 수 있도록 toString을 이용하기

LinkedList.java

```java
public String toString() {
		// 만약 데이터가 없다면 [] 출력
		if(head == null) {
			return "[]";
		}
		// 리스트로 순차적인 작업인 처리를 한다면 
		// 제일먼저 "head가 누군지"부터 찾아야 한다!
		Node temp = head;
		String str = "[";
		
		while(temp.next != null) {
			str += temp.data + ", ";
			temp = temp.next;
		}
		str += temp.data; // 마지막은 next가 없기 때문에 값을 수동으로 추가한다
		
		return str +"]";
	}
```

1. 리스트 안에 데이터가 없다면 [] 괄호만 출력되도록 한다
2. 데이터가 있다면 head부터 순차적으로 출력한다

```java
public static void main(String[] args) {
		LinkedList numbers = new LinkedList(); //링크드 리스트 인스턴스화
		numbers.addLast(10);
		numbers.addLast(20);
		numbers.addLast(30);
		numbers.add(1, 15);
		System.out.println(numbers);
	}
```

결과값 ⇒ [10, 15, 20, 30]

<br><br>

# 7. removeFirst

리스트의 첫번째 값을 삭제하는 numbers.removeFirst()를 구현한다

linkedList.java

```java
public Object removeFirst() {
		// 노드를 탐색해야하기 때문에 head값을 일단 찾아 temp에 넣는다
		Node temp = head;
		// head는 삭제될 거니까 다음 노드로 head를 옮긴다
		head = head.next;
		// 자바의 컬렉션에서 삭제하는 값을 리턴하듯, 
		// 우리도 삭제될 데이터 값을 returnData에 담아 리턴한다. 
		Object returnData = temp.data;
		temp = null;
		size--;
		return returnData;
	}
```

main.java

```java
public static void main(String[] args) {
		LinkedList numbers = new LinkedList(); //링크드 리스트 인스턴스화
		numbers.addLast(10);
		numbers.addLast(20);
		numbers.addLast(30);
		System.out.println(numbers.removeFirst()); // 잘 됐는지 확인
		System.out.println(numbers);
	}
```

결과값 ⇒ 

10
[20, 30]

- 삭제한 데이터값인 10과 삭제된 후의 리스트값인 [20,30]이 출력되었다.

<br><br>

# 8. remove, removeLast

### remove

특정한 위치에 있는 엘리먼트를 삭제한다.

- 삭제하려는 노드의 이전 노드를 알아야 한다. 삭제될 노드의 **이전 노드**가 next로 삭제하려는 노드의 다음 노드를 가리켜야 하기 때문에.
- 삭제하려는 노드 k -1을 알아내서 그걸 temp의 값으로 지정한다

linkedList.java

```java
public Object remove(int k) {// k는 인덱스 값
		if(k == 0) {
			return removeFirst();
		}
		Node temp = node(k-1);
		Node todoDeleted = temp.next; // 삭제하려는 노드
		temp.next = temp.next.next;
		Object returnData = todoDeleted.data;
		if(todoDeleted == tail) {// 삭제하려는 노드가 마지막 노드라면,
			tail = temp; // 삭제하려는 노드의 이전 노드이다
		}
		todoDeleted = null;
		size--;
		return returnData;
	}
```

main.java

```java
public static void main(String[] args) {
		LinkedList numbers = new LinkedList(); //링크드 리스트 인스턴스화
		numbers.addLast(5);		
		numbers.addLast(10);
		numbers.addLast(15);		
		numbers.addLast(20);
		numbers.addLast(30);
		System.out.println(numbers.remove(2)); // 잘 됐는지 확인
		System.out.println(numbers);
	}
```

결과값 ⇒

15
[5, 10, 20, 30]

### removeLast

```java
public Object removeLast() {
		return remove(size-1);
	}
```

- 위에서 만든 remove()를 이용해서 size-1을 넣어준다
- remove를 쓰면 앞에서부터 하나씩 찾아서 마지막까지 가야하는데, 어차피 tail에 마지막 노드의 정보가 들어있으니 그것만 삭제하면 안되나? → 안됨. 부족함
    - 그 이전 노드의 next값을 지워주어야지만 삭제된 효과가 있다. 즉, temp(이전 노드)를 알아야 한다!!
    - 그래서 가장 마지막 노드를 지운다는건 최악의 경우이다. (만약 데이터가 천만개라면 속도가 엄청나게 늦어질것임)
    - 반면, ArrayList는 내부적으로 index를 가지고 있다 ⇒ 배열의 마지막 인덱스값만 가지고 있으면 괭장히 빠르게 삭제를 처리할 수 있다.

main.java

```java
public static void main(String[] args) {
		LinkedList numbers = new LinkedList(); //링크드 리스트 인스턴스화
		numbers.addLast(5);		
		numbers.addLast(10);
		numbers.addLast(15);		
		numbers.addLast(20);
		numbers.addLast(30);
		System.out.println(numbers.removeLast()); // 잘 됐는지 확인
		System.out.println(numbers);
	}
```

결과값⇒

30
[5, 10, 15, 20]

<br><br>
## 9. size, get

- size() : 가지고 있는 엘리먼트의 갯수 구하기

    ```java
    public int size() {
    		return size;
    	}
    ```

    삭제하거나 추가할 때 마다 사이즈 값을 갱신해왔기 때문에 size값을 그냥 호출하면 된다.

- get(index) : 특정한 위치에 있는 엘리먼트를 가져올 때 사용
- Main.java

    System.out.println(numbers.get(1)); 

- LinkedList.java

    ```java
    public Object get(int k) {
    		Node temp = node(k); // 인덱스 값을 그대로 준다
    		return temp.data;
    	}
    ```

<br><br>

## 10. indexOf

특정한 데이터가 어떤 위치에 존재하는가를 검색.

Main.java

```java
public static void main(String[] args) {
		LinkedList numbers = new LinkedList(); //링크드 리스트 인스턴스화
		numbers.addLast(10);
		numbers.addLast(20);
		numbers.addLast(30);
		System.out.println(numbers.indexOf(30)); // 2를 리턴
	}
```

LinkedList.java

```java
public int indexOf(Object data) {
		Node temp = head;
		// 찾고자 하는 노드가 나올때까지 하나하나 검색
		int index = 0; // 찾고자하는 노드의 위치정보
		while(temp.data != data) { // temp에 저장된 데이터값과 검색하고자 하는 데이터값이 같지 않으면 계속 검색
			temp = temp.next; //다음 노드를 찾을 수 있도록
			index++;
			if(temp == null) {// 끝 노드에 도달했다면
				return -1;// 검색 종료
			}
		}
		return index;
	}
```

결과값 ⇒ 2


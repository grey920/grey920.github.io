---
title: "[자료구조] Array List 자바로 구현하기"
excerpt: 생활코딩 강의 정리 - Array List를 java로 구현한다
categories:
- DataStructure
tags:
- ArrayList
- java
toc: true
toc_sticky: true
toc_label: ArrayList 자바로 구현하기
---

# 1. 객체 생성하기

먼저 실행할 Main 클래스와 주인공인 ArrayList객체를 만든다.

 **Main.java**

```java
package list.arraylist.implementation;

public class Main {

	public static void main(String[] args) {

		// 새로운 ArrayList 객체 생성
		ArrayList numbers = new ArrayList();
	}

}
```

 **ArrayList.java**

```java
package list.arraylist.implementation;

// 배열을 내부적으로 사용하기 때문에 이름에 Array가 들어간다.
public class ArrayList {
	private int size = 0; // elementData 배열 안에 몇 개의 데이터가 들어있느냐를 알아낼 수 있는 변수
	
	//내부적으로 사용할 배열이기 때문에 private으로 감춘다.
	private Object[] elementData = new Object[100]; 
	// Object타입의 배열을 생성해서 elementData라 하는 비공개 접근자를 가진 인스턴스 변수에 할당한다. 
	// 그 배열은 100개의 데이터만 수용할 수 있다.
}
``` 
<br><br>

# 2. 데이터 추가하기

## 1) addLast - 마지막 위치에 추가

- 가장 끝에 데이터를 추가하는 메서드
- 비교적 가장 쉽다.

**Main.java**

```java
package list.arraylist.implementation;

public class Main {

	public static void main(String[] args) {

		ArrayList numbers = new ArrayList();
		numbers.addLast(10); // 리스트에 10이라는 값이 추가됨
		numbers.addLast(20); // ArrayList 내부에 있는 elementData의 가장 끝에 20이 추가됨
		numbers.addLast(30);
		numbers.addLast(40);
	}

}
```

**ArrayList.java**å

```java
package list.arraylist.implementation;

// 배열을 내부적으로 사용하기 때문에 이름에 Array가 들어간다.
public class ArrayList {
	private int size = 0; 
	
	private Object[] elementData = new Object[100]; 

	
	public boolean addLast(Object element) { 
		// 데이터는 elementData에 추가되어야 한다
		//size : 내부적으로 몇 개의 데이터가 채워졌느냐 (0으로 초기화 되어있다) 
		elementData[size] = element; 
		// elementData[0] = element -> addLast의 입력값으로 들어온 element가 elementData의 0번째 값이 된다.
		size++; //size가 1로 변함 
		return true;
	}
}
```

## 2) add - 중간에 추가

"만약 10과 20 사이에 15를 추가하고 싶다면??"

- 특정 위치에 데이터를 낑겨 넣고 싶다면 그 위치에 있는 엘리먼트를 포함한 모든 엘리먼트들을 한 칸씩 쭈욱 뒤로 밀어야 한다 → 할 일이 많다!! 시간이 오래 걸림 **(최대 단점)**
- 뒤로 데이터를 한 칸씩 옮기는 코드 작성
    - elementData[4] = elementData**[3]**; // size-1 
    elementData[3] = elementData[2];
    elementData[2] = elementData**[1]**; // index
    ⇒ 패턴을 찾아 **반복문**으로 바꾸기

![https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2892.png](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2892.png)

### add메서드 구현하기

```java
package list.arraylist.implementation;

// 배열을 내부적으로 사용하기 때문에 이름에 Array가 들어간다.
public class ArrayList {
	private int size = 0; 
	
	private Object[] elementData = new Object[100]; 

	
	public boolean addLast(Object element) { 
		elementData[size] = element; 
		size++; 
		return true;
	}
	public boolean add(int index, Object element) {
		for(int i = size - 1; i >= index; i--) { // 리스트의 가장 뒤부터 해당 인덱스까지 
			elementData[i + 1] = elementData[i]; // 하나씩 값을 뒤로 옮긴다
		}
		elementData[index] = element; // 비어있는 인덱스에 넣고싶었던 값을 넣는다. 
		size++;
		return true;
	}
}
```

## 3) 처음에 추가 (add 이용)

**Main.java**

```java
package list.arraylist.implementation;

public class Main {

	public static void main(String[] args) {

		// 새로운 ArrayList 객체 생성
		ArrayList numbers = new ArrayList();
		numbers.addLast(10); // 인덱스 0
		numbers.addLast(20); // 인덱스 1
		numbers.addLast(30);
		numbers.addLast(40);
		numbers.add(1, 15);//인덱스 번호 1 에 15를 인자로 준다
		numbers.addFirst(5); // 첫번째 위치에 5를 추가
	}

}
```

**ArrayList.java**

```java
package list.arraylist.implementation;

// 배열을 내부적으로 사용하기 때문에 이름에 Array가 들어간다.
public class ArrayList {
	private int size = 0; 
	
	private Object[] elementData = new Object[100]; 

	public boolean addFirst(Object element) {
		return add(0,element); // 이미 만든 add 메서드에 element 인자를 넣는다
	}
	
	public boolean addLast(Object element) { 
		elementData[size] = element; 
		size++; 
		return true;
	}
	public boolean add(int index, Object element) {
		for(int i = size - 1; i >= index; i--) { // 리스트의 가장 뒤부터 해당 인덱스까지 
			elementData[i + 1] = elementData[i]; // 하나씩 값을 뒤로 옮긴다
		}
		elementData[index] = element; // 비어있는 인덱스에 넣고싶었던 값을 넣는다. 
		size++;
		return true;
	}
	
}
```

- addFirst() 메소드에 리턴값으로 add()메소드를 이용한다. 매개변수로 0과 element를 보내면 add 메서드에서 모든 엘리먼트를 다 뒤로 보내고 인덱스 0번에 해당 element를 추가한다

<br><br>
# 3. 데이터 확인 - toString

> 객체 안에 포함되어있는 데이터가 정상적인 상태인지, 의도한 것과 같은지 확인하기

**Main.java**

```java
public static void main(String[] args) {

		// 새로운 ArrayList 객체 생성
		ArrayList numbers = new ArrayList();
		numbers.addLast(10); 
		numbers.addLast(20); 
		numbers.addLast(30);
		numbers.addLast(40);
		numbers.add(1, 15);
		numbers.addFirst(5); 
		
		System.out.println(numbers); // 기본적으로 객체의 레퍼런스 (객체의 위치값)이 나옴 
	}
```

**ArrayList.java**

```java
public String toString() { 
		//toString을 직접 구현하면 객체를 문자로 출력해야하는 상황에서 
		//toString이라는 메소드를 실행하도록 약속되어 있다.
		return "TEST";
	}
```

- console 출력 : 
 TEST

### 보기 좋게 출력하기

**ArrayList.java**

```java
public String toString() { 
		String str = "[";
		for (int i = 0; i < size; i++) {
			str += elementData[i];
			if(i < size-1) { // elementData갯수가 1 작은 숫자보다 i가 작다면 ,를 붙인다
				str += ",";
			}
		}
		return str + "]";
	}
```

- console 출력 : 
 [5,10,15,20,30,40]

<br><br>
# 4. 데이터 삭제

- 데이터를 추가하는 것과는 반대의 순서를 따름
- LinkedList보다 동작 속도가 느리다.

![https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2893.png](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2893.png)

- 리스트는 빈자리를 허용하지 않기 때문에 뒤를 다 앞 칸으로 땡겨서 옮겨야 한다.
- 인덱스 2번에서 1로 옮기는 것부터 시작해야 함.

**Main.java**

```java
package list.arraylist.implementation;

public class Main {

	public static void main(String[] args) {

		// 새로운 ArrayList 객체 생성
		ArrayList numbers = new ArrayList();
		numbers.addLast(10); 
		numbers.addLast(20); 
		numbers.addLast(30);
		numbers.addLast(40);
		System.out.println(numbers.remove(1)); // 20이 삭제되었기 때문에 리턴값 20이 출력되어야 함
		System.out.println(numbers);
	}

}
```

**ArrayList.java**

```java
package list.arraylist.implementation;

// 배열을 내부적으로 사용하기 때문에 이름에 Array가 들어간다.
public class ArrayList {
	private int size = 0; 
	
	private Object[] elementData = new Object[100]; 

	public boolean addFirst(Object element) {
		return add(0,element); 
	}
	
	public boolean addLast(Object element) { 
		elementData[size] = element; 
		size++; 
		return true;
	}
	public boolean add(int index, Object element) {
		for(int i = size - 1; i >= index; i--) {  
			elementData[i + 1] = elementData[i]; 
		}
		elementData[index] = element;  
		size++;
		return true;
	}
	
	public String toString() { 
		String str = "[";
		for (int i = 0; i < size; i++) {
			str += elementData[i];
			if(i < size-1) { 
				str += ",";
			}
		}
		return str + "]";
	}

	// Collection Framework remove메소드는 기본적으로 리턴값이 있다. (삭제한 엘리먼트의 저장되어있었던 값을 리턴해야 함)
	public Object remove(int index) { 
		Object removed = elementData[index]; //삭제하기 전에 값을 removed에 저장한다.  
		// 뒤에 있는 것들을 순차적으로 앞으로 땡겨줘야 한다.
		for(int i = index + 1; i <= size-1; i++) { //삭제하려는 인덱스 다음부터 i가 size-1보다 작거나 같은 동안에 (마지막 위치)까지 
			elementData[i-1] = elementData[i];
		}
		size--; // 데이터 삭제가 되었기 때문에 사이즈를 감소시킨다. 
		elementData[size] = null; // 삭제하고 데이터를 앞으로 옮기면 맨 뒤의 데이터가 하나 더 남아있게 된다. 맨 마지막 데이터는 없어야 하기 때문에 null로 지정한다.
		return removed; // 삭제한 값을 리턴한다
	}
	
}
```

## 2) 데이터를 앞뒤로 삭제하기 - remove() 리턴

**ArrayList.java**

```java
public Object remove(int index) { 
		Object removed = elementData[index];   
		for(int i = index + 1; i <= size-1; i++) {  
			elementData[i-1] = elementData[i];
		}
		size--;  
		elementData[size] = null;
		return removed; 
	}
	
	public Object removeFirst() {
		return remove(0);
	}
	
	public Object removeLast() {
		return remove(size-1);
	}
```

**Main.java**

```java
package list.arraylist.implementation;

public class Main {

	public static void main(String[] args) {

		// 새로운 ArrayList 객체 생성
		ArrayList numbers = new ArrayList();
		numbers.addLast(10); 
		numbers.addLast(20); 
		numbers.addLast(30);
		numbers.addLast(40);
		numbers.removeFirst(); // 출력값 : [20,30,40]
		//numbers.removeLast(); // 출력값 : [10,20,30]
		System.out.println(numbers);
	}

}
```

<br><br>
# 5. 데이터 가져오기 - get

- get은 인자로 전달된 인덱스 값을 그대로 **배열**로 전달한다. 배열은 인덱스를 통해 메모리의 주소에 직접 접근하는 랜덤 엑세스 이기 때문에 매우 빠르게 처리된다. ⇒ **ArrayList의 중요한 장점!**

**ArrayList.java**

```java
public Object get(int index) {
		return elementData[index];
	}
```

**Main.java**

```java
package list.arraylist.implementation;

public class Main {

	public static void main(String[] args) {

		// 새로운 ArrayList 객체 생성
		ArrayList numbers = new ArrayList();
		numbers.addLast(10); 
		numbers.addLast(20); 
		numbers.addLast(30);
		numbers.addLast(40);
		System.out.println(numbers.get(0));	
		System.out.println(numbers.get(1));	
		System.out.println(numbers.get(2));	
		System.out.println(numbers.get(3));	
	}

}
```

- 콘솔 출력 : 
10
20
30
40

<br><br>
# 6. 엘리먼트의 크기 - size(), indexOf()

- 현재의 리스트가 몇 개의 엘리먼트를 가지고 있는가
    - numbers.size();
    - ArrayList.java

    ```java
    // 변수로 직접 접근하지 않고 메소드를 사용하는 이유는?? -> 그래야 외부에서 size 변수값을 맘대로 바꾸지 못하니까
    	public int size() {
    		return size; // size 변수를 리턴
    	}
    ```

- 해당하는 값의 인덱스가 몇인가?
    - numbers.indexOf();
    - ArrayList.java

    ```java
    public int indexOf(Object o) {
    		// 리스트의 엘리먼트들을 하나씩 순회한다.
    		for(int i=0; i<size; i++) {
    			//해당하는 엘리먼트가 o와 같은지 확인 
    			if(o.equals(elementData[i])) {
    				return i;
    			}
    		}
    		// 찾을 수 없다면
    		return -1; // 찾는 값이 없다는 뜻!
    	}
    ```

<br><br>

# 7. 반복

- 리스트도 배열처럼 데이터의 집합이기 때문에 반복적으로 처리하는 작업이 꼭 필요하다.

### 1) 반복문

```java
for(int i=0; i < numbers.size(); i++) {
			System.out.println(numbers.get(i));
		}
```

- 콘솔 출력 : 
10
20
30
40

### 2) Iterator (권장됨)

- 반복적인 작업을 위해 고안된 객체를 사용하는 방법

**Main.java**

```java
// 반복작업을 위해서 ListIterator라는 객체가 필요하다. ListIterator객체를 리턴받기 위해서 listIterator()메소드를 사용
		ArrayList.ListIterator li = numbers.listIterator(); // 리턴되는 객체를 li에 담는다.
		System.out.println(li.next()); //10
		System.out.println(li.next()); //20
		System.out.println(li.next()); //30
		System.out.println(li.next()); //40
```

**ArrayList.java**

```java
// 1)
	public ListIterator listIterator() { //ListIterator는 리턴할 데이터 타입
		return new ListIterator();
	}

	
	// 2) ArrayList클래스 안에 ListIterator 클래스 생성
	class ListIterator{
		private int nextIndex = 0;
		public Object next() {
			Object returnData = elementData[nextIndex]; // 리턴값은 ListIterator의 부모 클래스인 ArrayList의 elementData배열에 담겨있다.
								// elementData[nextIndex] : 리턴할 특정 인덱스는 next()메소드가 호출될때마다
								// 인덱스의 값이 0을 시작으로 1씩 증가한다면 elementData에 담겨있는 값들을 
								// 순차적으로 하나씩 꺼내서 리턴할 수 있다
			nextIndex++;
			return returnData;
		} 
		 
	}
```

리턴값을 elementData[nextIndex++]로 바꿈으로써 next()메소드를 한 줄로 더 간단히 고칠 수 있다. 

```java
class ListIterator{
		private int nextIndex = 0;
		public Object next() {
			return elementData[nextIndex++];
		} 
	}
```

메인에서 next()메소드를 더 사용하면 **null**이 출력된다. 

→ 더 이상 가져올 값이 없기 때문에!

```java
ArrayList.ListIterator li = numbers.listIterator(); // 리턴되는 객체를 li에 담는다.
		System.out.println(li.next()); //10
		System.out.println(li.next()); //20
		System.out.println(li.next()); //30
		System.out.println(li.next()); //40
		System.out.println(li.next());
		System.out.println(li.next());
```

- 콘솔 출력 : 
10
20
30
40
null
null

- 메인의 반복적인 next()를 반복문으로 바꿔 자동화 시키기

```java
while(true) { 
			System.out.println(li.next());
		}
```

이렇게 하면 배열의 모든 값이 출력됨과 동시에 **에러**까지 출력된다.

- 배열의 최대값인 100을 넘어간 값까지 출력을 요구하기 때문에 ArrayIndexOutOfBoundsException이 출력

따라서 while의 조건에 hasNext()를 만들어서 반복의 종료 조건을 설정한다.

```java
while(li.hasNext()) { //hasNext()가 true일때만 실행
			System.out.println(li.next());
		}
```

### 3) hasNext()

**ArrayList.java**

```java
class ListIterator{
		private int nextIndex = 0;
		
		public boolean hasNext() { 
						// size()와 nextIndex의 값을 비교해서 
						// nextIndex가 더 작으면 next()호출해서 어떤 엘리먼트를 가져올 수 있는 상태라는걸 true로 리턴
			return nextIndex < size();
		}
		
		public Object next() {
			return elementData[nextIndex++];
		} 
	}
```

- 배열의 크기(size())와 nextIndex를 비교해서 다음 출력값이 없을때까지 계속 반복하도록 만든다.

### 4) previous와 hasPrevious

- 이전 엘리먼트를 찾는 기능

**ArrayList.java**

```java
public Object previous() {
			return elementData[--nextIndex];
		}
		
		public boolean hasPrevious() {
			return nextIndex > 0;
		}
```

**Main.java**

```java
ArrayList.ListIterator li = numbers.listIterator(); 
		while(li.hasNext()) {
			System.out.println(li.next());
		}
		
		while(li.hasPrevious()) {
			System.out.println(li.previous());
		}
```

- 콘솔 출력 : 
10
20
30
40
40
30
20
10

### 5) Iterator add, remove

**Iterator add**

**Main.java**

```java
ArrayList.ListIterator li = numbers.listIterator(); 
		while(li.hasNext()) {
			int number = (int)li.next();
			if(number == 30) {
				li.add(35);
			}
		}
		System.out.println(numbers);
```

- 값이 30일때 35를 리스트에 추가하는 코드.

**ArrayList.java**

ListIterator 클래스 안

```java
public void add(Object element) {
			ArrayList.this.add(nextIndex++, element);
			// 그냥 add라고 쓰면 현재의 add메소드가 나오기 때문에
			// this를 써서 numbers에 포함된 add메소드임을 나타낸다
		}
```

- 콘솔 출력 : 
[10,20,30,35,40]

**Iterator remove**

```java
public void remove() { // nextIndex가 가리키는 인덱스의 이전 인덱스를 지운다.
			ArrayList.this.remove(nextIndex-1);
			nextIndex--;
		}
```

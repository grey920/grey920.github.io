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
---
title: "[자료구조] Array List"
excerpt: Array List 설명
categories:
- DataStucture
tags:
- Array
toc: true
toc_sticky: true
toc_label: ArrayList
---

ArrayList?? 리스트를 만들 때 내부적으로 **배열**을 사용하는 것. ← 내부적으로는 배열이 사용되고 있기 때문에 배열의 인덱스를 이용하여 데이터를 가져온다!

# 자바에서 ArrayList 사용하기

자바는 컬렉션 프레임워크라는 자체적인 라이브러리 안에 ArrayList data structure를 기본적으로 내장하고 있다. ⇒ 따라서 ArrayList **사용법**을 익히자!

[여기](https://www.youtube.com/playlist?list=PLuHgQVnccGMDsWOOn_P0EmAWB8DArS3Fk)서 강의 확인 가능합니다.

## 1. ArrayList 생성하기

```java
ArrayList<Integer> numbers = new ArrayList<>();
```

1) new 연산자를 사용하여 ArrayList 객체를 만들고

2) 1로 만든 것을 ArrayList타입의 변수인 numbers에 할당한다.

*<Integer> 제네릭을 쓰는 이유? ⇒ 사용하려는 ArrayList가 내부적으로 엘리먼트들이 숫자라는 것을 미리 지정함.

## 2. 데이터 추가하기

```java
numbers.add(1,50);
```

- "1번 인덱스에 50이라는 값을 끼워넣고 싶다"

## 3. 데이터 삭제하기

```java
numbers.remove(2);
```

## 4. 인덱스를 통해 데이터 가져오기

```java
numbers.get(2);
```

## 5. 데이터의 사이즈 가져오기

몇 개의 엘리먼트가 저장되어 있는지 알고 싶을 때 사용.

```java
numbers.size();
```

# Iteration 반복 사용하기

Iterator it = numbers.iterator();

ArrayList에 저장되어 있는 데이터를 순차적인 반복 작업을 통해 요소들 하나하나를 꺼내 와서 어떤 처리를 하는 것! 

- numbers : ArrayList 객체
- iterator() : numbers 객체가 가지고 있는 iterator() 메서드를 호출. 리턴값이 Iterator 타입이다.
- Iterator : 인터페이스
- it : 리턴값들이 담기는 변수

## 1) while

```java
Iterator it = numbers.iterator();
	while(it.hasNext()){
		int value = (int)it.next();
	}
}
```

## 2) for each

```java
for(int value : numbers){
	System.out.println(value);
}
```

## 3) for

```java
for(int i=0; i < numbers.size(); i++){
	System.out.println(numbers.get(i));
}
```

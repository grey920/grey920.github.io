---
title: "자바에서의 함수형 프로그래밍"
excerpt: "자바의 근본은 객체지향 아입니까?(긁적)"
categories:
    - Server
tags:
  - java
  - 함수형 프로그래밍
  - Functional Interface
  - StreamAPI
  - Lambda
  - 글또
toc: true
toc_sticky: true
toc_label: "자바에서의 함수형 프로그래밍"
toc_icon: "edit"
# classes: wide
header:
  teaser: 'https://storage.googleapis.com/jjalbot/2021/12/FIJNHwO7f/FIJNHwO7f.jpeg' #/assets/images/2022-01-02/Untitled.png
---

## 이  글을 쓰게 된 동기
“함수형 프로그래밍" 책으로 사내 스터디를 진행했었습니다. 이 책에서의 예제는 javascript 언어로 되어있었습니다. 제가 실무에서 가장 많이 접하고, 객체 지향으로 설계된 Java에서는 함수형 프로그래밍이 어떻게 적용될 수 있을지 이번 기회에 직접 써보며 공부해보고 싶었습니다.

## 함수형 프로그래밍이란
**함수형 프로그래밍** (functional programming)은 자료 처리를 수학적 함수의 계산으로 취급하고 상태와 가변 데이터를 멀리하는 프로그래밍 패러다임의 하나입니다. 
명령형 프로그래밍에서는 상태를 바꾸는 것을 강조하는 것과는 달리, 함수형 프로그래밍은 함수의 응용을 강조합니다. 프로그래밍이 문이 아닌 식이나 선언으로 수행되는 `선언형 프로그래밍` 패러다임을 따르고 있습니다. ( [출처](https://ko.wikipedia.org/wiki/%ED%95%A8%EC%88%98%ED%98%95_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D) )

### 자바에서의 객체지향 vs 함수형
가장 큰 차이는 **값을 취급하는 단위**가 어디까지인지에 따라 나눌 수 있습니다.

-   객체지향 - **상태(값)** 와 행위(메서드)를 담기 위한 기본 단위를 객체로 정의했고, 이 객체를 클래스라는 형태로 구현할 수 있습니다.
-   함수형 - **행위** 에 해당하는 부분도 **값으로 취급**이 가능하다는 말은 자바의 기본형 데이터 (Integer, String 등)만 값이 아니라 **행위(로직)도 값으로 취급할 수 있게 되었다**는 것입니다. **(일급값)**

객체지향 프로그래밍이 객체간 메세지와 협력 관계의 정의로 이루어졌다면, 함수형 프로그래밍은 함수들의 조합으로 이루어집니다.

자바가 8부터 *함수형 개발 패러다임을 지원함*으로서 자바가 코드의 재활용 단위가 클래스였던 것이 함수 단위로 재사용이 가능해지면서 조금 더 개발을 유연하게 할 수 있게된 점이라 할 수 있습니다.

### 왜  함수형 프로그래밍이 필요할까
반도체 성능 향상의 한계에 다다르자 CPU 회사들은 하나의 칩 속도를 높이는 방식 대신, 여러 개의 칩이 `병렬적으로 동작`하도록 하여 성능을 높이는 방식을 선택했습니다.

이로 인해 어플리케이션 코드는 멀티쓰레드를 이용하여 CPU의 코어를 최대한 활용해야만 하는 환경이 되었습니다. 멀티쓰레드를 활용한 동시성 프로그래밍은 교착상태에 빠질 위험이 존재합니다.
이러한 문제가 발생하는 주 원인은 스레드 간에 공유되는 데이터나 상태 값이 변경 가능한 **mutable한 상태**이기 때문입니다.

이런 환경에서 함수형 프로그래밍은 모든 데이터가 변경 불가능하고 부수 효과를 관리하기 때문에 여러 쓰레드가 동시에 공유 데이터에 접근하더라도 해당 데이터가 변경될 수 없어 병렬 프로세스나 쓰레드에 안전합니다.

또한 추상화 레벨이 높아짐에 따라 필요한 정보만 나타내고 복잡한 것을 숨기기 때문에 전체적인 흐름을 파악하는데 더 용이합니다.

## 함수형 패러다임
객체지향 언어의 특징을 이야기할 때 보통 객체지향의 4대 요소 (다형성, 추상화, 캡슐화, 상속성) 나 SOLID(SRP, OCP, LSP, ISP, DIP)와 같은 5대 원칙을 말하곤 합니다.
함수형 프로그래밍 역시 중요한 핵심 키워드가 있습니다.
<img src="https://user-images.githubusercontent.com/58028215/235812116-1bfec121-6a54-4bcf-a5bb-6110a8f338d0.png">

### 1) Pure Function. 순수 함수
순수 함수란 **같은 입력에 대해 항상 같은 출력을 반환**하는 함수입니다.

또한 전역 변수를 사용하거나 변경함으로 인한 예상치 못한 부수효과가 발생하지 않습니다. 따라서 멀티쓰레드에서도 안전하고 병렬처리 및 계산도 가능합니다.
```java
private String name = "grey";
@Test
@DisplayName( "순수 함수 예제" )
public void pure_function(){

	// 순수함수 call
	System.out.println( greeting_pure( name ) );

	// 순수함수X
	System.out.println( greeting_not_pure() );
}

public static String greeting_pure( String name ){
	return "Hello" + name;
}

public String greeting_not_pure(){
	// 전역 변수 사용
	return "Hello" + name;
}
```



### 2) No Iterate. 반복문을 사용하지 않는다
for, while과 같은 반복문을 사용하지 않습니다. 자바에서는 반복문 대신 Stream API를 사용하거나 재귀함수를 작성하여 기존에 for문으로 처리했던 많은 일들을 보다 간결한 코드로 작성할 수 있게 합니다.

> 퍼포먼스가 중요하거나 반복 횟수가 매우 크다면 표준 루프를 사용하는게 좋습니다.<br> 컴파일러가 기존 for-loop는 오랫동안 사용해왔기 때문에 최적화를 잘하지만 스트림은 최적화를 잘 하지 못한다고 합니다.


```java
@Test
@DisplayName( "반복 없음 예제" )
public void no_iterate(){
	List<Integer> numbers = List.of( 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 );

	// for loop
	for ( int i = 0; i < numbers.size(); i++ ) {
			System.out.print( numbers.get( i ) );
	}

	System.out.println("\n------------------");

	// functional
	numbers.forEach( num -> System.out.print( num ) );

}
```

### 3) High Order Function. 고차 함수
고차함수란 함수를 인자로 받거나 함수를 반환값으로 이용할 수 있는 함수입니다.

Java8에서 추가된 **`함수형 인터페이스`**(단일 추상 메서드를 가지는 인터페이스)를 이용하면 함수를 객체로서 다룰 수 있습니다.
자바의 Stream API는 forEach, map, filter 등과 같은 고차함수들을 제공합니다.

아래의 예시는 함수를 반환하는 고차함수 예시입니다.
```java
@Test
@DisplayName( "고차 함수 예제" )
public void test () {

    // greetingText 함수 : 인사말을 입력받아 함수로 반환합니다. 반환하는 함수는 이름을 인자로 받아 상위 함수의 입력받은 인사말을 붙여 출력하는 함수입니다.
    Function<String, Function<String, String>> greeting = ( greetingText ) -> {
            return ( name ) -> {
										// 외부 함수의 값인 greetingText에 접근하고, scope가 종료해도 계속 접근할 수 있습니다.(Hello, Hi를 각각 유지) -> 클로저
                    return greetingText + " " + name;
            };
    };

    Function<String, String> hello = greeting.apply( "Hello" );
    Function<String, String> hi = greeting.apply( "I am " );

    System.out.println( hello.apply( "grey" ) );
    System.out.println( hi.apply( "grey" ) );

}

>> Hello grey
>> I am  grey
```

> `클로저` <br>
> 클로저는 내부함수가 외부함수의 context에 접근할 수 있는 것을 말합니다.
> 
> 또한 외부함수가 종료되더라고 내부함수에서 참조하는 외부함수의 context는 유지됩니다.
> 
> 예시에서 제일 아래 출력되는 라인을 보면 hello.apply(), hi.apply()에서 이미 종료된 외부 함수의 greetingText에 여전히 참조할 수 있는 것을 볼 수 있습니다.
> <br>
> <br>
> 내부함수가 사용하는 외부함수의 지역변수를 클로저가 생성되는 시점에 final로 간주됩니다.<br> 
> 자바1.8 이후부터는 외부함수의 지역변수는 유사 final로 간주되어 명시적으로 붙이지 않아도 컴파일 타임에 final로 간주되어 새로운 인스턴스를 할당하지 못하게 되는 것입니다.


### 4) Immutability. 불변성
불변성은 변할 수 없는 값을 의미합니다. 자바에서 값 타입 변수들은 final로 선언하면 값 변경시 컴파일 에러가 발생하지만, 참조 변수들은 final 선언으로 재할당을 막을 순 있어도 원소에 값을 추가할 수 있습니다. → 이는 불변성이 있다고 할 수 없습니다.
```java
@Test
@DisplayName( "불변성 예제" )
public void immutability() {
	final String name = "grey";
//                name = "정겨운"; // 컴파일 에러

	final List<String> family = new ArrayList<String>(Arrays.asList( "정겨운", "정다와", "정중기", "이미자" ));
	family.add( "강동원" );

	System.out.println( "family = " + family );
}

>> family = [정겨운, 정다와, 정중기, 이미자, 강동원]
```
<img src="https://user-images.githubusercontent.com/58028215/235812788-0174dc5f-b118-4402-9b5d-7873d4bccca2.png">

이럴때 Collection 객체들은 Collections.unmodifiableList()를 사용하면 불변성 객체로 만들 수 있습니다. 또는 DeepCopy를 해서 새로운 요소를 추가하면서 불변성을 보장할 수도 있습니다 .
```java
final List<String> realFamily = Collections.unmodifiableList( new ArrayList<String>(Arrays.asList(  "정겨운", "정다와", "정중기", "이미자" )));
realFamily.add( "강동원" );
```


## 자바의 함수형 인터페이스
### 1) 함수형 인터페이스란?
[오라클에서의 함수형 인터페이스 정의](https://docs.oracle.com/javase/specs/jls/se8/html/jls-9.html#jls-9.8)
<img src="https://user-images.githubusercontent.com/58028215/235812879-dbb5eb65-1edb-4f69-9e06-47b4b72ccb03.png">
함수형 인터페이스는 **단 하나의 추상 메서드를 가지는 인터페이스**입니다. "단 하나의 추상 메서드"는 Single Abstract Method, 줄여서 `SAM`이라 부르기도 합니다.

함수형 인터페이스는 함수를 일급 객체로 사용할 수 없는 자바 언어의 단점을 보완하기 위해 `자바 8`부터 도입되었습니다.
[java.util.function 패키지](https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html)는 자바에서 기본적으로 제공하는 함수형 인터페이스 패키지입니다.


> `❓단 하나만 가진다구요??`
> 
> 자바 8부터 하위호환성과 유연성 때문에 default 메서드 또는 static 메서드가 추가 정의할 수 있게 되었으므로 추상 메서드에 default 메서드와 static 메서드는 카운트에 포함시키지 않습니다.


java.util.function 패키지에 있는 IntPredicate 인터페이스를 예시로 보겠습니다.
```java
@FunctionalInterface
public interface IntPredicate {

    /**
     * Evaluates this predicate on the given argument.
     *
     * @param value the input argument
     * @return {@code true} if the input argument matches the predicate,
     * otherwise {@code false}
     */
    boolean test(int value);

    /**
     * Returns a composed predicate that represents a short-circuiting logical
     * AND of this predicate and another.  When evaluating the composed
     * predicate, if this predicate is {@code false}, then the {@code other}
     * predicate is not evaluated.
     *
     * <p>Any exceptions thrown during evaluation of either predicate are relayed
     * to the caller; if evaluation of this predicate throws an exception, the
     * {@code other} predicate will not be evaluated.
     *
     * @param other a predicate that will be logically-ANDed with this
     *              predicate
     * @return a composed predicate that represents the short-circuiting logical
     * AND of this predicate and the {@code other} predicate
     * @throws NullPointerException if other is null
     */
    default IntPredicate and(IntPredicate other) {
        Objects.requireNonNull(other);
        return (value) -> test(value) && other.test(value);
    }

    /**
     * Returns a predicate that represents the logical negation of this
     * predicate.
     *
     * @return a predicate that represents the logical negation of this
     * predicate
     */
    default IntPredicate negate() {
        return (value) -> !test(value);
    }

    /**
     * Returns a composed predicate that represents a short-circuiting logical
     * OR of this predicate and another.  When evaluating the composed
     * predicate, if this predicate is {@code true}, then the {@code other}
     * predicate is not evaluated.
     *
     * <p>Any exceptions thrown during evaluation of either predicate are relayed
     * to the caller; if evaluation of this predicate throws an exception, the
     * {@code other} predicate will not be evaluated.
     *
     * @param other a predicate that will be logically-ORed with this
     *              predicate
     * @return a composed predicate that represents the short-circuiting logical
     * OR of this predicate and the {@code other} predicate
     * @throws NullPointerException if other is null
     */
    default IntPredicate or(IntPredicate other) {
        Objects.requireNonNull(other);
        return (value) -> test(value) || other.test(value);
    }
}
```

IntPredicate 인터페이스를 보면 int형 인자를 받아 boolean 값을 리턴하는 test라는 메서드가 **하나** 존재하고, 이 외의 메서드들에는 모두 `default` 키워드가 붙은 default 메서드임을 확인할 수 있습니다.


> `@FunctionalInterface 애노테이션`
> 붙이지 않아도 함수형 인터페이스로 인식은 되지만 붙이는 편이 더 명시적이고, 컴파일러가 단일 추상화 메서드인지 검사할 수 있기 때문에 오류를 방지할 수 있다는 장점이 있어 붙여주는게 좋습니다.


### 2) 함수형 인터페이스의 종류
자바에서 제공하는 함수형 인터페이스의 종류는 다음과 같습니다.

|종류|인자|반환|설명|
|:---:|:---:|:---:|:---:|
|Runnable| | |기본적인 형태의 인터페이스, 인자와 반환값 모두 없음|
|Supplier\<T>| |\<T> |인자X. 제너릭 타입의 반환값만 있는 인터페이스, 항상 같은 값을 반환|
|Consumer\<T>| \<T>| |제너릭 타입의 인자만 있고 반환값이 없는 인터페이스|
|Predicate\<T>|\<T> | Boolean|제너릭 타입의 인자와 Boolean 타입의 반환값을 가지는 인터페이스|
|Function<T,R>| \<T>|\<R> |제너릭 타입의 인자와 다른 제너릭 타입의 반환값이 같이 있는 인터페이스|
|UnaryOperator|\<T>| \<T>| 같은 제너릭 타입의 인자와 반환값을 가지고 있는 인터페이스|
|BinaryOperator\<T>|<T,T> | \<T>|같은 제너릭 타입의 인자 2개를 받고 같은 제너릭 타입의 반환값을 가지는 인터페이스|
|BiConsumer<T,U>|<T,U>| |다른 제너릭 타입의 인자 2개를 받고 반환값이 없는 인터페이스|
|BiFunction<T,U>|<T,U> |Boolean |다른 제너릭 타입의 인자 2개를 받고 Boolean 타입의 반환값을 가지는 인터페이스|
|BiFunction<T,U,R>|<T,U> | \<R>|다른 제너릭 타입의 인자 2개를 받고 다른 제너릭 타입의 반환값을 가지는 인터페이스|
|Comparator\<T>| <T,T>| int|같은 제너릭 타입의 인자 2개를 받고 Integer 반환값을 가지는 인터페이스, 객체간의 값을 비교하기 위한 compare 기능을 위한 인터페이스|



### 3) 어떻게 단일 추상메서드로 고차 함수가 가능할까
인터페이스에 추상 메서드가 하나라고 하면 **인터페이스 구현 자체가 하나의 메서드 구현만을 의미**하므로 마치 함수와 같은 개념으로 이해할 수 있으며, `람다식`을 이용해 함수를 구현할 수 있습니다.



## 내 생각
- 책에서는 자바스크립트로만 나와서 과연 객체지향 언어인 자바에서도 효율적으로 함수형 프로그래밍을 할 수 있을까 싶었는데, 자바 8에서 제공하는 기능들을 사용하면 충분히 함수형으로 코딩할 수 있겠다라는 생각이 들었습니다,,
- 지금까지 개발하면서 filter나 map 등 반복문을 사용하는 경우에 `StreamAPI`를 자주 사용해왔습니다. 그러나 이게 `함수형 프로그래밍`과 어떤 상관관계가 있는지 생각하지 않고 단순히 사용법만 익혀서 쓰고 있었습니다.
	- StreamAPI는 Collection이나 array등과 같은 데이터소스에서 요소를 처리하는데 사용됩니다. 
	- 람다식은 이름없는 함수를 만들어 코드의 가독성을 높이고, 복잡한 처리를 간결하게 표현하는데에 사용됩니다. 이러한 람다 표현식은 함수형 인터페이스를 구현하는 데에 사용될 수 있습니다. 
	- `StreamAPI`을 통해 데이터를 처리하는 과정에서 `람다식`을 사용하여 함수를 전달하고, 이를 조립하여 처리 과정을 구성하게 됩니다.
	- 🔥 즉, StreamAPI 자체가 함수형 프로그래밍 개념을 Java에 적용한 것으로 볼 수 있습니다. 
- 처음 실무에서 stream을 사용하면서 로컬 변수의 **값을 변경**해야 하는 경우가 발생했었는데 (반복문을 돌면서 반복 횟수를 세는 경우), 이 때 'Variable used in lambda expression should be final or effectively final' 이라는 에러가 발생해서 당황한 적이 있었습니다. 
	- 해당 에러가 발생하는 근본적인 이유는 메모리 구조 때문이었습니다. ( 쓰레드 차이 )
	- 로컬 변수는 스택 영역에 생성되고 이 스택 영역을 쓰레드마다 별도의 스택이 생성됩니다. (쓰레드끼리 공유 X )
	- 람다는 별도의 쓰레드에서 실행이 가능합니다. 여기서 람다가 로컬 변수에 접근하는 경우, 다른 쓰레드의 스택 영역에 직접 접근하는 것이 아니라 해당 변수를 자신의 쓰레드 스택에`복사`하기 때문에 동일한 값을 참조할 수 있습니다.
	- 하지만 변수를 복사해서 사용하기 때문에 그 변수의 값이 중구난방으로 변경된다면 멀티 쓰레드 환경에서 동시성 이슈를 대응할 수 없습니다. 따라서 로컬 변수는 final이거나 final처럼 동작해야 한다는 제약 조건이 생긴 것입니다. -> `람다 캡처링`
	- 저는 당시에 다중 쓰레드에 안전하게 작업할 수 있도록 제공된 `AtomicInteger`를 사용해서 문제를 해결했었습니다. 다음에는 AtomicInteger와 쓰레드에 대한 이야기를 정리해봐야겠다는 생각이 드네요! 😀




## 출처(참고문헌)
-   ⭐`FP와 람다`: [자바](https://dinfree.com/lecture/language/112_java_9.html)
- 함수형 인터페이스란: [Functional Interface란](https://tecoble.techcourse.co.kr/post/2020-07-17-Functional-Interface/)
- 자바로 함수형 인터페이스 사용하기: [자바로 함수형 인터페이스 사용하기 (Functional Interface)](https://jogeum.net/18)
- High Order Function, 함수형으로 바꾸기: [자바코드로 보는 함수형 프로그래밍 (Functional Programming in Java)](https://warpgate3.tistory.com/entry/%EC%9E%90%EB%B0%94%EC%BD%94%EB%93%9C%EB%A1%9C-%EB%B3%B4%EB%8A%94-%ED%95%A8%EC%88%98%ED%98%95-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-Functional-Programming-in-Java)
- 자바 함수형 기술: [자바 함수형 프로그래밍 기술 7가지](https://sthwin.tistory.com/21)
- 자바 클로저,람다, 커링: [Java - 자바 클로져(Closure) & 커링(currying)](https://coding-start.tistory.com/370)
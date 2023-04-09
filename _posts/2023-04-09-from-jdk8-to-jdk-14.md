---
title: "JDK 8에서 JDK17로 업그레이드"
excerpt: "SI 한복판에서 JDK 17을 외치다..."
categories:
  - Server
tags:
  - JDK8
  - JDK17
  - 글또
toc: true
toc_sticky: true
toc_label: 목차
toc_icon: "list"
header:
  overlay_image: /assets/images/hero_background.jpg
  teaser: https://user-images.githubusercontent.com/58028215/226168839-9703102b-3ea9-4fe8-8a47-0b256b9c0740.png
---
## JDK란?
JDK는 **Java Development Kit**의 약자로, 이름 그대로 자바 애플리케이션을 개발할 때 필요한 도구들을 모아놓은 키트입니다. 
개발에 필요한 컴파일러나 디버거, 테스트 등의 개발 도구들을 가지고 있으며, 개발할 때 자바 프로그램을 구동을 해야하므로 자바 실행 환경인 JRE를 포함하고 있습니다.

JDK가 **컴파일러를 제공**하기 때문에 **사용하는 JDK가 코드를 작성할 수 있는 자바 버전을 결정합니다.** 
예를 들어 자바 8의 람다식을 사용하려면 컴파일을 위해 최소 JDK 8이 필요합니다. 그렇지 않으면 javac 명령이 구문 오류를 표시하면서 해당 코드를 거부하게 됩니다.

참고로, JDK를 제공하는 곳은 크게 두 가지로, 폐쇄적인 상업 코드 기반의 OracleJDK와 오픈소스로 운영 중인 OpenJDK가 있습니다. 
이 둘은 동일한 기반을 사용하므로 실질적인 기술 차이는 없습니다. 하지만 성능에 관해서는 OracleJDK는 기업 고객에게 서비스를 제공하기 때문에 안정성에 중점을 더 두고 있어 응답성 및 JVM 성능면에서 OracleJDK가 훨씬 좋습니다.
이 둘의 가장 큰 차이점은 상용인 OracleJDK는 유료이지만 오픈소스인 OpenJDK는 무료라는 점입니다. 또한 OracleJDK는 LTS 업데이트 지원을 받을 수 있지만, OpenJDK는 LTS 없이 6개월마다 새로운 버전이 배포됩니다.


## JAVA 8 버전의 특징
Java 8은 2014년 3월에 출시되었습니다. 
Java 8이 출시된 지 9년이 지났지만 여전히 인기가 많은 이유 중 하나는 Oracle JDK 지원 기간이 그 후에 나온  LTS 버전인 Java 11이나 Java 17보다 더 길기 때문입니다. (Extended Support) <br>

<img width="634" alt="image" src="https://user-images.githubusercontent.com/58028215/226168839-9703102b-3ea9-4fe8-8a47-0b256b9c0740.png"> <br>
[Oracle Java SE Support Roadmap](https://www.oracle.com/java/technologies/java-se-support-roadmap.html)

또한 자바는 대표적인 객체지향형 프로그램이지만 Java 8부터는 함수형 프로그래밍을 지원했습니다.<br>
대표적인 기능과 특징으로는 다음이 있습니다.
- 람다 표현식 : 함수형 프로그래밍
- 함수형 인터페이스와 디폴트 메서드
- 스트림 API : 데이터 추상화
- java.time 패키지 : Joda-Time을 이용한 새로운 날짜와 시간 API
- 병렬 배열 정렬
- Optional
- Base64 인코딩/디코딩 지원

그 외에도 메타 스페이스 영역이 추가되었고 G1GC에서의 변화가 있습니다.


## 왜 기존에 쓰던 JDK 1.8을 버리고 JDK 17로 가야할까?

<img width="498" alt="image" src="https://user-images.githubusercontent.com/58028215/226164087-fcaa501e-af06-4e9a-97ae-24bed6524a38.png"><br>
[Which versions of Java do you regularly use?](https://www.jetbrains.com/lp/devecosystem-2022/java/#which-versions-of-java-do-you-regularly-use-two-years)

- 위에서 봤던 표를 다시 보자면, 현재 가장 일반적으로 사용되는 Java 버전인 `Java8이 22년 3월 오라클 프리미어 지원이 종료`되었습니다. 이게 새로운 업데이트를 받지 못한다는건 아니지만, 유지보수에 대한 오라클의 노력이 지금보다 훨씬 줄어들 가능성이 높다는 것을 의미합니다.
- 또한 Oracle Java와 고가의 Java SE 구독에 한해서 Java8의 기능이 일부 확장이 있기 떄문에 유의미한 확장이라 볼 수 없습니다.
- **Java 17**은 2021년 9월 14일에 출시되었습니다. 이 버전은 새로운 LTS 버전으로, **오라클 프리미어 지원이 최소 2026년 9월까지 지속**됩니다.
<img width="634" alt="image" src="https://user-images.githubusercontent.com/58028215/226168839-9703102b-3ea9-4fe8-8a47-0b256b9c0740.png"><br>
[Oracle Java SE Support Roadmap](https://www.oracle.com/java/technologies/java-se-support-roadmap.html)

## JDK 17의 새로운 기능과 개선점
먼저, Java API를 버전 간 비교하고 싶다면, [Java Version Almanac](https://javaalmanac.io/)를 확인해 보면 좋습니다. 이곳에서 Java API의 추가 및 삭제 등 변경 사항들을 확인해볼 수 있습니다.
JDK 17의 기능은 [여기서](https://openjdk.org/projects/jdk/17/) 확인할 수 있습니다.

다음은 자바 8에서 17로 가기까지 어떤 변화가 있는지 살펴보겠습니다.


### var 키워드
타입을 추론하여 **지역 변수**를 보다 간결한 방식으로 선언할 수 있도록 `var` 라는 새로운 키워드가 추가되었습니다.
```java
// java 8 way
Map<String, List<MyDtoType>> myMap = new HashMap<String, List<MyDtoType>>();
List<MyDomainObjectWithLongName> myList = aDelegate.fetchDomainObjects();

// java 10 way
var myMap = new HashMap<String, List<MyDtoType>>();
var myList = aDelegate.fetchDomainObjects()
```
`var`를 사용하면 변수 타입을 명시하지 않아 훨씬 간결하고, 그 덕분에 가독성이 좀 더 좋아졌습니다.
하지만 경우에 따라서는 타입을 숨기는 것이 프로그래머에게 오히려 잘못된 경우가 있을 수 있으니 변수명을 올바르게 지어야 합니다.

[제약]<br>
`var 키워드`를 사용하여 변수에 **람다**를 할당할 수는 없습니다.
```java
// causes compilation error:
// method reference needs an explicit target-type
var fun = MyObject::mySpecialFunction;
```

하지만 람다 표현식 안에서 var 키워드를 사용할 수는 있습니다.
```java
boolean isThereAneedle = stringsList.stream().anyMatch((@NonNull var s) -> s.equals(“needle”));
```
람다 인자에 var를 사용하면 인자에 애노테이션을 추가할 수 있습니다.



### Record
[참고](https://www.baeldung.com/java-record-keyword)<br>
이전에는 DTO 클래스처럼 DB 쿼리 결과나 서비스 정보 등의 데이터를 단순히 보관하기 위해 클래스를 작성했습니다.
이러한 데이터 클래스의 데이터는 동기화 없이도 데이터의 유효성을 보장하기 위해 대부분 **불변성**을 지닙니다. 불변성을 가지기 위해 우리는 데이터 클래스를 만들때 다음처럼 만듭니다.
- 각 데이터에 대한 private final 필드
- 각 필드에 대한 getter
- 각 필드에 해당하는 인자를 가진 public 생성자
- equals 메소드 : 모든 필드가 일치할 때 동일한 클래스의 객체에 대해 true를 반환
- hashCode 메소드 : 모든 필드가 일치할 때 동일한 값을 반환
- toString 메소드 : 클래스의 이름과 각 필드의 이름 및 해당 값을 포함하는 문자열을 반환

이러한 작업들은 boilerplate 코드(상용구 코드)입니다.
record는 인스턴스에서 데이터를 설정하고 가져오는데 필요한 모든 상용구 코드를 없애는 것을 목표로 하는 특별한 타입의 클래스입니다. ( [JEP-395](https://openjdk.org/jeps/395) )

예를 들어, 일반적으로 name과 address라는 필드를 가진 Person 클래스를 만들어보면 다음과 같습니다.
```java
public class Person {

    private final String name;
    private final String address;

    public Person(String name, String address) {
        this.name = name;
        this.address = address;
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, address);
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) {
            return true;
        } else if (!(obj instanceof Person)) {
            return false;
        } else {
            Person other = (Person) obj;
            return Objects.equals(name, other.name)
              && Objects.equals(address, other.address);
        }
    }

    @Override
    public String toString() {
        return "Person [name=" + name + ", address=" + address + "]";
    }

    // standard getters
}
```
하지만 JDK 14부터는 반복적인 데이터 클래스를 record로 대체할 수 있습니다.
`record`는 **필드 유형**과 **이름**만 필요하고, 상용구이던 equals(), hashCode(), toString(), private, final 필드와 public 생성자는 자바 컴파일러에 의해 생성됩니다.

`record` 키워드를 사용하여 Person record를 만든 모습은 다음과 같습니다.
```java
public record Person (String name, String address) {}
```
record 클래스를 사용하면 컴파일러가 헤더를 통해 내부 필드를 추론하여 자동으로 구현을 하기 때문에 코드가 훨씬 간결해집니다.

[제약]
- 모든 필드가 private final로 선언되기 때문에 **상속**이 불가능합니다.
- **setter**를 통해 값을 설정해야 하는 경우 사용할 수 없습니다.


### switch 표현식의 확장
switch-case는 **break** 키워드가 없어져 훨씬 더 읽기 쉬운 방식으로 그룹화가 가능하며 switch 표현식 자체가 결과를 반환하게 되었습니다. ( case문에 **람다식**도 지원된다구여..! )
```java
DayOfWeek dayOfWeek = LocalDate.now().getDayOfWeek();

boolean freeDay = switch (dayOfWeek) {

	case MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY -> false;
	
	case SATURDAY, SUNDAY -> true;

};
```

게다가 **yield** 키워드를 함께 사용하면 코드 블럭 내의 값을 리턴할 수 있습니다. 
```java
DayOfWeek dayOfWeek = LocalDate.now().getDayOfWeek();

boolean freeDay = switch (dayOfWeek) {

	case MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY -> {
	
		System.out.println("Work work work");
		
		yield false;
	
	}
	
	case SATURDAY, SUNDAY -> {
	
		System.out.println("Yey, a free day!");
		
		yield true;
	
	}

};
```
이러면 case블럭 내부에서 switch문의 결과값을 셋팅하여 리턴하게 됩니다.


### 🔥 instanceof 패턴 매칭
*[프리뷰 기능..!!](https://docs.oracle.com/en/java/javase/17/language/pattern-matching-switch-expressions-and-statements.html)*<br>
기존에는 객체가 특정 구조를 가지고 있어도 해당 구조로 형변환을 해야했지만, 패턴 매칭을 사용하면 형변환 없이 바로 객체로부터 데이터를 추출할 수 있습니다.
```java
if (obj instanceof MyObject) {
	MyObject myObject = (MyObject) obj;
	// … further logic
}
```
이전에는 MyObject 타입으로 다시 형변환을 해야했습니다. 

```java
if (obj instanceof MyObject myObject) {
	// … the same logic
}
```
하지만 이젠 if 조건문 안에서 형변환 없이 바로 지역 변수로 myObject에 접근할 수 있습니다.

```java
if (obj instanceof MyObject myObject && myObject.isValid()) {
	// … the same logic
}
```
이 경우 조건부 AND 연산자는 단락 연산자이기 때문에 instanceof가 true인 경우에만 프로그램이 `myObject.isValid()`  식에 접근할 수 있습니다. 


### 🔥 sealed 클래스 (봉인 클래스)
**sealed** 클래스 또는 인터페이스는 해당 클래스/인터페이스의 **상속/구현을 제한**합니다. ( [JEP 409](https://openjdk.org/jeps/409) )
이를 통해 개발자는 *어떤 클래스가 해당 클래스를 상속받는지 쉽게 알 수 있습니다.*

- 방법은 super class에 `sealed 키워드`를 사용하고, `permits` 키워드 뒤에 해당 클래스를 상속받을 sub class를 선언합니다. 
- sealed 된 클래스를 사용하기 위해서는 같은 모듈, 혹은 같은 패키지 안에 존재해야 합니다. 
- 활용 권한을 받은 sub class는 sealed / non-sealed / final 총 세가지 종류로 나뉩니다
	- `sealed` : permits로 선언된 클래스만 상속.
	- `non-sealed` : 어떤 서브 클래스든 상속. 즉, 어떠한 서브 클래스라도 자식으로 둘 수 **있다.** 
	- `final` : final 클래스는 상속을 금지시킨다. 즉, 어떠한 클래스도 자식으로 둘 수 `없다.` 

```java
public sealed class Shape permits Circle, Square, Rectangle {
}
```
다음을 보면 sealed 클래스인 Shape 클래스가 있고 이 클래스는 permits 키워드를 통해 Circle, Square, Rectangle 클래스만이 상속을 받을 수 있도록 지정했습니다. ( 세 클래스는 같은 모듈에 있다고 가정합니다 )

1. final 클래스 Circle
```java
public final class Circle extends Shape {
    public float radius;
}
```
Circle은 final 클래스이기 때문에 다른 클래스는 Circle를 상속할 수 없습니다. 

2. non-sealed 클래스 Square
```java
public non-sealed class Square extends Shape {
   public double side;
}  
```

3. sealed 클래스 Rectangle
```java
public sealed class Rectangle extends Shape permits FilledRectangle {
    public double length, width;
}
```
Rectagle 클래스는 또 다른 서브 클래스인 FilledRectagle 클래스를 가집니다.
```java
public final class FilledRectangle extends Rectangle {
    public int red, green, blue;
}
```



### TextBlock
`텍스트 블록`은 Java의 여러 줄의 문자열을 간편하게 작성할 수 있도록 합니다. ( [JEP 378](https://openjdk.org/jeps/378) )
이러한 텍스트 블록을 통해 json 또는 xml 템플릿을 더욱 읽기 쉽게 만들 수 있습니다. 
- `"""{문자열}"""`  형식으로 사용합니다.

HTML 예시의 경우, 기존에는 쌍따옴표와 escape 문자로 개행을 구현했습니다. 
```java
String html = "<html>\n" +
              "    <body>\n" +
              "        <p>Hello, world</p>\n" +
              "    </body>\n" +
              "</html>\n";
```

하지만 텍스트 블록을 사용하면 다음과 같이 더욱 가독성있게 작성할 수 있습니다. 
```java
String html = """
              <html>
                  <body>
                      <p>Hello, world</p>
                  </body>
              </html>
              """;
```


### 나아진 NullPointerExceptions
다음과 같이 체이닝으로 값을 꺼내는 경우 중간에 NPE가 발생해도 해당 라인이라는 것만 알고, 정확히 어디에서 발생하는지는 알 수 없었습니다. 
```java
company.getOwner().getAddress().getCity();
```

이제는 에러 메시지가 구체적으로 표시되고, JVM이 `Person.getAddress()를 호출할 수 없습니다.` 라고 정확하게 알려줍니다.


### 새로운 Optional.orElseThrow() method
Optional에서 get() 메서드 사용시 값이 없으면 예외가 발생합니다.
```java
MyObject myObject = myList.stream()
	.filter(MyObject::someBoolean)
	.filter((b) -> false)
	.findFirst()
	.get();
```

if문으로 Optional 객체의 유무를 판단하는 것보다 Java 10에 새로 추가된 `orElseThrow()`를 사용하면 get()과 똑같이 동작하지만 개발자에게 좀 더 명확하게 값이 없으면 에러가 발생함을 알려줄 수 있습니다.
```java
MyObject myObject = myList.stream()
	.filter(MyObject::someBoolean)
	.filter((b) -> false)
	.findFirst()
	.orElseThrow();
```


### 그 외 API 변화들
```java
// Predicate에 not과 static import (::)를 사용해서 코드를 더 간결하게 쓸 수 있다.
collection.stream()
	.filter( Predicate.not( MyObject::isEmpty ) )
	.collect( Collectors.toList() );

// String에 추가된 method : isBlank, strip, indent
“\nPretius\n rules\n all!”.repeat(10).lines().
	.filter( Predictions.not( String::isBlank ) )
	.map( String::strip )
	.map( s -> s.indent(2) )
	.collect( Collectors.toList() );

// List를 Array로 변환시 인자로 List의 인스턴스를 보내지 않아도 된다. 대신 배열 생성자 참조를 보낸다. ( array constructor reference )
String[] myArray= aList.toArray( String[]::new );

// read and write to files quickly!
// remember to catch all the possible exceptions though
Path path = Files.writeString( myFile, "Pretius Rules All !" );
String fileContent = Files.readString( path );

// .toList() on a stream()
String[] arr={"a", "b", "c"};
var list = Arrays.stream(arr).toList();
```


## 업그레이드시 주의해야 할 점
JDK8에서 JDK17로 업그레이드하면서 제거된 기능들이 있습니다. 예를 들어, JDK 17에서는 java.security.acl 패키지와 관련된 클래스와 메서드가 제거되었습니다. 이러한 클래스와 메서드를 사용하고 있다면 코드를 업데이트해야 합니다.<br>
또한 호환성 문제도 있습니다. 의존성 라이브러리가 JDK 17과 호환되지 않을 수 있습니다. 






# 출처(참고문헌)
- JDK
	- ["JDK란 무엇인가" 자바 개발 키트 소개와 설치하기](https://raptor-hw.net/xe/know/168921)
	- [JAVA8 변경 사항](http://www.tcpschool.com/java/java_intro_java8)
- G1GC
	- [Java HotSpot VM G1GC](https://johngrib.github.io/wiki/java-g1gc/)
- [Java 17 features: A comparison between versions 8 and 17. What has changed over the years?](https://pretius.com/blog/java-17-features/)
- [JDK 17 발표 및 새로운 변화](https://blogs.oracle.com/javakr/post/jdk-17)
- [우리팀이 JDK 17을 도입한 이유](https://techblog.gccompany.co.kr/%EC%9A%B0%EB%A6%AC%ED%8C%80%EC%9D%B4-jdk-17%EC%9D%84-%EB%8F%84%EC%9E%85%ED%95%9C-%EC%9D%B4%EC%9C%A0-ced2b754cd7)
- [oracle ::: Java Language updates](https://docs.oracle.com/en/java/javase/17/language/java-language-changes.html)
- Record 
	- [Java record Type with Examples](https://howtodoinjava.com/java14/java-14-record-type/)
	- [자바의 레코드(Record)](https://scshim.tistory.com/372)
	- [\[Java\]자바 record를 entity로?](https://velog.io/@power0080/java%EC%9E%90%EB%B0%94-record%EB%A5%BC-entity%EB%A1%9C)
- instanceof 패턴 매칭
	- [Java Language Updates - Pattern Matching for instanceof](https://docs.oracle.com/en/java/javase/17/language/pattern-matching-instanceof-operator.html)
- sealed class
	- [Java 17,Sealed Class](https://velog.io/@wwe221/Java-17-Sealed-Class)
- 그 외 API 변화들
	- [String API Updates in Java 12](https://www.baeldung.com/java12-string-api)


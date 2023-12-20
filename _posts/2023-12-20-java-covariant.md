---
title: "자바에서 공변성(covariance), 반공변성(contravariance) 그리고 무변성 (invariance)"
excerpt: ""
categories:
  - Server
tags:
  - Java
  - covariant
toc: true
toc_sticky: true
toc_label: "자바에서 공변성, 반공변성 그리고 무변성"
toc_icon: "edit"
# classes: wide
header:
  teaser: /assets/images/2023/12-20/자바의공변.png #/assets/images/2022-01-02/Untitled.png
---

## 글을 쓰게 된 이유
- 멘토님과 StringBuffer와 StringBuilder에 대해 소스 코드를 보면서 이야기를 나누다가 두 클래스 모두 AbstractStringBuilder 추상 클래스를 **상속**받고 있음을 확인했다.
- **override**하면 리턴 타입이나 파라미터 등 부모의 메소드 선언부를 그대로 **동일**하게 가져가야 하는 줄 알았는데 자식 클래스의 **리턴 타입**이 **더 상세**한 것이다..! 아니 리턴 타입이 달라도 돼..?
<figure>
  <img src='https://github.com/grey920/grey920.github.io/assets/58028215/1154f683-0ee0-4ddc-af53-7a2062e4f851'>
  <img src='https://github.com/grey920/grey920.github.io/assets/58028215/0e00985d-79eb-4b9c-9cd0-1dde768e87c6' width='450'>
  <img src='https://github.com/grey920/grey920.github.io/assets/58028215/09907ae9-bc87-4d93-b482-1852f30a3e11' width='450'>
  <figcaption>AbstractStringBuilder와 StringBuffer, StringBuilder의 append메소드</figcaption>
</figure>


- 여기서 멘토님이 `covariance(공변)`라는 키워드를 주셔서 이번 기회에 좀 더 알아보기로 한다.

## 공변, 반공변, 무변성?
갑자기 왜 **공변**이라는 키워드가 나왔을까? 

<figure>
  <img width="567" alt="image" src="https://github.com/grey920/grey920.github.io/assets/58028215/4a78771b-8c1e-4b43-b9d0-20d82cd9bdc7">
  <figcaption></figcaption>
</figure>

위의 AbstractStringBuilder와 StringBuffer, StringBuilder는 **상속관계**에 있다. <br>
그리고 이 **관계의 흐름과 동일**하게 자식 타입의 리턴 타입(StringBuffer, StringBuilder)이 부모 타입의 리턴 타입(AbstractStringBuilder)보다 상세한 것을 확인할 수 있다. <br>
이렇게 계층 관계에서 타입 간에 어떤 관계가 있는지를 나타내는 것을 `변성`이라 한다.

<figure>
  <img width="650" alt="image" src="https://github.com/grey920/grey920.github.io/assets/58028215/77142158-f17d-4c1d-bbfa-5aedd5894eb5">
  <figcaption>Inheritance in object-oriented languages</figcaption>
</figure>

그리고 이러한 변성에는 공변, 반공변, 무공변이 있다. (Bivariance는 여기서 다루지 않을 예정) <br>
이해를 돕기 위해 예시로 List를 들어본다.


### 공변 (Covariance)
클래스간 관계가 제네릭 타입의 구조에도 동일하게 적용된다. 
말그대로 기존 클래스 관계를 따라 제네릭 구조도 **함께**(`공`) **변한다**(`변`) . <br>
객체지향 프로그래밍에서 [리스코프 치환 원칙](https://ko.wikipedia.org/wiki/%EB%A6%AC%EC%8A%A4%EC%BD%94%ED%94%84_%EC%B9%98%ED%99%98_%EC%9B%90%EC%B9%99) 이 여기에 해당한다. 

<figure>
  <img width="450" alt="image" src="https://github.com/grey920/grey920.github.io/assets/58028215/a53ae71f-4dbd-4be8-a14c-ec57d052ac77">
  <figcaption></figcaption>
</figure>
```java
Animal a = new Tiger(); // OK  
  
List<Animal> animalList = new ArrayList<>();  
List<Tiger> tigerList = new ArrayList<>();  
animalList = tigerList; // compile X
```
예를 들어 `Tiger`가 `Animal`의 하위 타입일 때 `List<Tiger>`는 `List<Animal>`의 하위 타입이라면 **공변**하다고 본다. <br>
자바의 **제네릭**은 기본적으로 `무공변(invariance)`이기 때문에 위와 같은 관계가 성립되지 않는다. 
그럴 때 자바에서는 `? extends T` 키워드를 사용해서 공변을 사용할 수 있다. <br>
예를 들어, `List <? extends Animal>` 는 Animal 또는 Animal의 하위 타입을 요소로 가지는 리스트를 의미한다.

```java
List<? extends Animal> animalList = new ArrayList<>();  
List<Tiger> tigerList = new ArrayList<>();  
animalList = tigerList; // compile O
```

### 반공변 (Contravariance)
반공변은 공변과 반대로, 제네릭 타입의 구조가 클래스간 관계와 반대로 적용될 때를 의미한다. 

<figure>
  <img width="460" alt="image" src="https://github.com/grey920/grey920.github.io/assets/58028215/a9afa4f2-f99d-431e-9456-3e3e7c3c11e2">
  <figcaption></figcaption>
</figure>

```java
List<Animal> animalList = new ArrayList<>();  
List<Tiger> tigerList = new ArrayList<>();  
tigerList = animalList; // compile X
```
예를 들어 `Tiger`가 `Animal`의 하위 타입일 때 `List<Tiger>`가 `List<Animal>`의 상위 타입이라면 **반공변**하다고 본다.
자바에서는 `? super T` 키워드를 사용해서 반공변을 사용할 수 있다. <br>
예를 들어 `List<? super Tiger>`는 Tiger 또는 Tiger의 상위 타입을 요소로 가지는 리스트를 의미한다. 
```java
List<Animal> animalList = new ArrayList<>();  
List<? super Tiger> tigerList = new ArrayList<>();  
tigerList = animalList; // compile O
```

### 무공변/불변 (Invariance)
다른 타입은 받을 수 없고 오직 해당 타입만 받는 경우를 의미한다. 
자바의 **제네릭**이 기본적으로 이 경우에 해당한다.
<figure>
  <img width="465" alt="image" src="https://github.com/grey920/grey920.github.io/assets/58028215/bbee0da1-cc39-40f5-9dce-ef31dc6dd7f4">
  <figcaption></figcaption>
</figure>
예를 들어 `Tiger`가 `Animal`의 하위 타입일 때 `List<Tiger>`와  `List<Animal>`가 아무런 관계가 없는 경우 무공변에 해당한다. 


## 자바에서의 공변, 반공변, 무변성

### 4가지 시나리오
자바에서는 공변과 반공변, 무변성이 어디에 어떻게 적용되어 있을까?
다음 예시를 보자. 
아래와 같은 상속 관계를 가진 클래스가 있다.
<figure>
  <img width="550" alt="image" src="https://github.com/grey920/grey920.github.io/assets/58028215/f8827b2f-0176-4ae7-8260-dbe27492a9e2">
  <figcaption></figcaption>
</figure>


```java
public class Animal {  
}  

class Carnivore extends Animal {  
}  
  
class Tiger  extends Carnivore {  
}  
  
class Lion extends Carnivore {  
}
```

이 때 `변수 선언시`, `메소드 override 시`, `배열`일 때와 `제네릭`일 때 각각 어떻게 적용되는지 알아보자. 

#### 1) 변수 선언문
자바에서 변수를 선언할 때는 **공변**이다. 
상속 관계에서 형변환(Casting)시  **"서브 타입은 언제나 기반 타입으로 교체할 수 있어야 한다."** 는 `리스코프 치환 원칙`이 기본 매커니즘이기 때문에 아주 익숙하다.
```java
// Tiger는 Animal이다. ( 상속은 covariant : LSP )
Animal animal = new Carnivore();  
Animal animal2 = new Tiger();  
Carnivore carnivore = new Tiger();
```

#### 2) 메소드 재정의
자바에서 메소드 override시 **리턴 타입**은 **공변**이지만 *파라미터*는 *무공변*이다.
인터페이스를 구현하는 메소드를 코드로 살펴보자.
먼저 `AniInterface`라는 인터페이스를 만들고, 최상위 타입인 **Animal**을 매개 변수로 받고, 리턴 타입으로 보내는 `getAnimal()`이라는 메소드를 만들었다.
```java
  
public interface AniInterface {  
    public Animal getAnimal( Animal animal);  
}  
  
// 1. work!  
class AniInterfaceImpl implements AniInterface {  
    public Carnivore getAnimal( Animal animal) {  
        return new Carnivore();  
    }  
}  
  
// work...!!!!  
class AniInterfaceImpl2 implements AniInterface {  
    public Carnivore getAnimal( Animal animal) {  
        return new Tiger();  
    }  
}  
  
// NOT work  
class AniInterfaceImpl3 implements AniInterface {  
    public Animal getAnimal( Carnivore carnivore ) {  
        return new Animal();  
    }  
}
```
자바는 리턴 타입으로 공변을 지원하기 때문에 재정의한 메소드에서 더 구체적인 타입을 반환할 수 있다. 
1. 재정의한 메소드에서 **하위 타입(Carnivore) 리턴** -> OK
2. 재정의한 메소드에서 리턴 타입은 하위 타입으로 정의, **실제로는 하위의 하위 타입(Tiger) 리턴** -> OK

하지만 3.은 **파라미터 타입**이 Animal의 하위인 Carnivore이다. 
자바에서 파라미터 타입은 `무공변`이기 때문에 **Overload**된 메소드로 여기게 된다. 
<figure>
  <img width="650" alt="image" src="https://github.com/grey920/grey920.github.io/assets/58028215/c914f8d7-08eb-4286-9f21-9e26c75ff253">
  <figcaption></figcaption>
</figure>

즉, 재정의한 `파라미터 타입`이 부모와 동일하지 않으면 **다른 메소드로 인식**되기 때문에 컴파일러가 부모 메소드를 구현하라고 에러를 발생한다.

#### 3) 배열
자바에서 **배열**은 `공변`이다.  따라서 Animal이 Carnivore의 상위 타입이기 때문에 Animal[] 역시 Carnivore[]의 상위 타입이 된다.
```java
Animal[] animals = new Carnivore[10];  
Animal[] animals2 = new Tiger[10];  
Carnivore[] carnivores = new Tiger[10];  
  
animals2[0] = new Carnivore();
```

배열이 공변이기 때문에 컴파일 에러없이 코드를 작성할 수 있지만,
반대로 공변이기 때문에 위의 코드는 **초기화된 타입이 아닌 요소를 배열에 담을 수 있어서** 잠재적으로 `ArrayStoreException`이 발생할 위험을 가지고 있다. 

<figure>
  <img width="650" alt="image" src="https://github.com/grey920/grey920.github.io/assets/58028215/2762e733-dee4-456a-8230-c7d591c0d85d">
  <figcaption></figcaption>
</figure>

인텔리제이에서는 IDE 수준에서 "배열에 초기화에 사용한 타입과 다른 타입의 요소를 넣으면 Exception이 발생한다"고 경고를 주고있다. 
<figure>
  <img width="650" alt="image" src="https://github.com/grey920/grey920.github.io/assets/58028215/0f907f26-e950-45bb-9d81-b94af675a845">
  <figcaption></figcaption>
</figure>

실제로 실행해보면 Tiger 타입의 객체만을 저장하기 위한 배열에 Carnivore 타입의 객체를 할당하려고 시도했기 때문에 경고했던 `ArrayStoreException`이 발생한다. 

이 경우 `List<Animal>` 과 같이 **제네릭 컬렉션**을 사용하면 `타입의 범위를 설정`할 수 있기 때문에 컴파일 때에도 타입 안정성을 보장할 수 있고, 런타임시에도 오류의 가능성을 줄일 수 있다.

#### 4) 🌟 제네릭 컬렉션
먼저, 제네릭은 기본적으로 **무변성**이다. 즉, 같은 타입만을 받는다. 
따라서 `Cage<T>` 라는 클래스가 있을 때 `Animal`이 `Tiger`보다 상위클래스라 할지라도 `Cage<Animal>`에 `Cage<Tiger>`를 할당할 수는 없다. 

```java
Animal animal = new Tiger(); // OK

Cage<Animal> ca1 = new Cage<Tiger>(); // 컴파일 에러
Cage<Animal> ca2 = new Cage<Animal>(); // OK
```

예를 들어 육식 동물 케이지에 먹이를 주는 사육사 클래스를 만들어보자.
```java
public class Zookeeper {  
  
    /**  
     * invariant type parameter     
     * @param cage  
     * @param m  
     */  
    public void feed(Cage<Carnivore> cage, Meat m) {  
        System.out.println("Feeding animals in cage > invariant type parameter");  
    }

	static class Meat {  
    }
}
```

그리고 먹이를 주는 코드를 작성한다.
```java
Zookeeper zk = new Zookeeper();  
Cage<Tiger> ct = new Cage<>();  
zk.feed( ct, new Zookeeper.Meat() ); // ct에서 컴파일 에러!
```
<figure>
  <img width="806" alt="image" src="https://github.com/grey920/grey920.github.io/assets/58028215/ee5feddd-1b91-4aeb-b80e-3c1912cf1d78">
  <figcaption></figcaption>
</figure>

feed() 메소드의 첫번째 파라미터로 `Cage<Carnivore>` 타입을 받고 있는데 넘겨준 타입은 관계가 없는 `Cage<Tiger>` 이기 때문에 feed()는 값을 받을 수 없다. 


이걸 받게 하기 위해 만약  Zookeeper의 feed() 메소드 파라미터를 실제 원하는 하위타입으로 각각 만들면 어떨까?
<figure>
  <img width="345" alt="image" src="https://github.com/grey920/grey920.github.io/assets/58028215/8b43cbf7-4027-4afe-824c-7f67f6a3e233">
  <figcaption></figcaption>
</figure>

그럼 사용하는 쪽에서는 의도한대로 컴파일 에러는 발생하지 않는다. <br>
하지만 제공하는 쪽에서는 컴파일 에러가 발생한다. 
<figure>
  <img width="650" alt="image" src="https://github.com/grey920/grey920.github.io/assets/58028215/f1f629fc-00ff-485d-b8fa-b4d2515a7e5f">
  <figcaption></figcaption>
</figure>

메소드 오버로딩을 기대했지만 이 경우엔 'both methods have same **erasure**' 라는 컴파일 에러를 준다. <br>
✨제네릭은 컴파일 시점에 타입 정보를 체크하고 **런타임**에는 이 정보를 **제거**한다. 
그렇기 때문에 feed() 메소드가 런타임 시점에는 `Cage<Tiger>` 와 `Cage<Lion>` 모두 단순히 `Cage` 클래스로 취급되기 때문에 **동일한 시그니처를 가진 메소드**로 간주된다.

내가 원한 동작은 Zookeeper의 feed() 메소드에서 **육식 동물에 해당하는 우리**에 고기를 던져주는 행위일 뿐이다. <br>
즉, `육식 동물 우리에 고기를 준다` == `육식 동물에 속하는 호랑이와 사자가 있는 우리에 고기를 준다` 가 성립되길 원하는 것이다. => 🌟 제네릭의 무공변을 **공변**하게 만들고 싶다!

### 제네릭에서 무공변을 공변하게 만들기
일반적인 컬렉션 동작을 변경하려면, 메소드 파라미터와 같이 사용하는 위치에서 명시적으로 `? extends U` 를 사용해서 제네릭을 **공변**으로 만든다.
`? extends U` 는 타입 매개변수의 범위가 U 클래스이거나, U의 자식 타입만 가능하다는 뜻이다. 
```java
/**  
 * covariant type parameter 
 * 파라미터 T가 적어도 Carnivore 를 상속한 타입임이 보장됨.  
 * @param cage  
 * @param m  
 */  
public void feed(Cage<? extends Carnivore> cage, Meat m){  
    System.out.println("Feeding animals in cage > covariant type parameter" + cage.getAllAnimals() );
}
```
이제  Zookeeper의 feed() 메소드는 와일드카드(`?`) 와 `extends` 를 통해서 Carnivore 클래스와 Carnivore 클래스를 상속받는 클래스들을 모두 Cage의 제네릭 타입으로 받을 수 있게 되었다.<br>
즉, cage의 타입이 아무리 높아봤자(?!) Carnivore 타입까지임을 보장받는다. ( **상한 경계** )

그럼 이제 다시 고기를 줘보자
```java
/* 무변성 invariant 일 때 문제 -> 공변 covariant 로 해결 (Zookeeper의 feed 메소드의 파라미터에 extends 추가) */  
Zookeeper zk = new Zookeeper();  
Cage<Tiger> ct = new Cage<>();  
ct.addAnimal( new Tiger() );  
zk.feed( ct, new Zookeeper.Meat() ); // feed 메소드의 파라미터 Cage<? extends Carnivore> 타입에 Cage<Tiger> 할당 가능  
  
Cage<Lion> cl = new Cage<>();  
cl.addAnimal( new Lion() );  
zk.feed( cl, new Zookeeper.Meat() ); // feed 메소드의 파라미터 Cage<? extends Carnivore> 타입에 Cage<Lion> 할당 가능  
  
Cage<Carnivore> cc = new Cage<>();  
cc.addAnimal( new Carnivore() );  
zk.feed( cc, new Zookeeper.Meat() ); // feed 메소드의 파라미터 Cage<? extends Carnivore> 타입에 Cage<Carnivore> 할당 가능
```

컴파일 에러도 발생하지 않고 실행도 잘 된다.
<figure>
  <img width="635" alt="image" src="https://github.com/grey920/grey920.github.io/assets/58028215/77229170-d960-46f4-b708-19b421863fbb">
  <figcaption></figcaption>
</figure>


feed() 메소드를 제공하는 Zookeeper 클래스 쪽에서 `? extends` 로 제네릭 타입을 공변하게 받도록 처리함으로써 한 번에 자식 클래스 제네릭 타입도 받을 수 있게 되었다. 


#### 🔥공변일 때 문제점 : extends 로 공변한 타입은 메소드에 값 전달이 안된다..!!

그럼 이제 육식 동물 케이지에 사자와 호랑이를 넣어보자.
```java
// Cage<? extends Carnivore> 에 Cage<Tiger>를 할당 => 가능
Cage<Tiger> ct2 = new Cage<>();  
Cage<? extends Carnivore> cage = ct2;

cage.addAnimal( new Tiger() ); // 컴파일 에러
```
<figure>
  <img width="575" alt="image" src="https://github.com/grey920/grey920.github.io/assets/58028215/51560f40-ff8f-4533-9726-700812d44519">
  <figcaption></figcaption>
</figure>

cage.addAnimal( new Tiger() ); 에서 컴파일 에러가 발생한다. <br>
이는 자바 컴파일러가 `? extends Carnivore`가 **무엇인지 정확히 알 수 없기 때문에 발생**하는 `안전성 문제`이다.

Cage 클래스 입장에서 생각해보자. addAnimal()의 파라미터 타입으로 **T타입**이 온다고 선언했는데, 사용하는 쪽(호출부)에서 `? extends Carnivore` 타입을 보내고 있다.
(물론 런타임에는 정보가 소거되지만 일단 이해하기 쉽도록..!)<br>
그럼 Cage 클래스는 인자로 `Tiger` 타입이 올지, `Lion` 타입이 올지, `Carnivore` 타입이 올지 **알 수가 없다**. → 안전하지 않으니 컴파일 에러 발생!🚨


#### 🔧 가능한 처리법 
컴파일 에러를 없애려면 어떻게 할까

1) 정확히 알 수 있게 **타입을 명시적으로 지정**한다.
```java
Cage<Tiger> tigerCage = new Cage<>();  
tigerCage.addAnimal( new Tiger() );  
  
Cage<Lion> lionCage = new Cage<>();  
lionCage.addAnimal( new Lion() );
```
이렇게 명시적으로 알려주면 컴파일러 입장에서는 어떤 값이 들어오는지 정확히 알 수 있기 때문에 에러를 뱉지 않는다. <br>
하지만 Tiger와 Lion 제네릭 타입을 따로 만들지 않고 한 번에 처리할 수 없을까?

2) Cage **클래스 타입 수정**
```java
public class Cage <T extends Carnivore> {  
    private List<T> animals = new ArrayList<>();  
  
    public void addAnimal( T animal ) {  
        animals.add( animal );  
        System.out.println( "Adding animal to cage > " + getAllAnimals() );  
    }  
  
    public List<T> getAllAnimals() {  
        return animals;  
    }  
  
}
```
`Cage <T extends Carnivore>`라고 클래스 선언부에 명시하여 Cage 클래스의 제네릭 타입이 Carnivore와 그 하위 타입만 받도록 설계한다.

```java
Cage<Carnivore> carnivoreCage = new Cage<>();  
carnivoreCage.addAnimal( new Tiger() );  
carnivoreCage.addAnimal( new Lion() );
```
사용할 때 Carnivore 타입의 케이지를 생성하고 그 안에 Tiger와 Lion을 넣어도 문제가 발생하지 않는다.

3) **제네릭 메소드**로 수정
```java
public <U extends T> void addAnimal( U animal ) {  
    animals.add( animal );  
    System.out.println( "Adding animal to cage > " + getAllAnimals() );  
}
```
addAnimal() 메소드 선언시 리턴 타입 앞에 **제네릭한 타입( `<U extends T>`)을 선언** 하고, 그 타입을 매개 변수에서 사용한다.

```java
Cage<Carnivore> cage = new Cage<>();  
cage.addAnimal( new Tiger() ); // OK
```
이제 addAnimal() 호출부에서 구체적인 타입을 지정해줄 수 있다. <br>
위의 코드에서는 `Cage<Carnivore> cage = new Cage<>();` 를 통해 Cage 클래스의 제네릭 타입(`T`)이 Carnivore 타입으로 인식된다.
따라서 addAnimal( U animal ) 에서 U 는 `<U extends Carnivore>` 를 만족해야 한다.

만약 `U extends T` 에 해당하지 않는 타입을 인자로 넣어 호출하면 다음과 같이 컴파일 에러가 발생한다.
<figure>
  <img width="810" alt="image" src="https://github.com/grey920/grey920.github.io/assets/58028215/3ab2bcdc-39aa-41d4-99a9-295bee9535f4">
  <figcaption></figcaption>
</figure>
  
### 제네릭에서 공변을 반공변하게 만들기
또 다른 해결법으로는 반공변하게 만드는 것이다. 
`? super U` 는 타입 매개변수의 범위가 U 클래스이거나, U의 부모 타입만 가능하다는 뜻이다. 
```java
// AS-IS
public void addAnimal( T animal ) {  
    animals.add( animal );  
    System.out.println( "Adding animal to cage > " + getAllAnimals() );  
}

// TO-BE
public void addAnimal( Cage<? super T> cage, T animal ) {  
    animals.add( animal );  
    System.out.println( "Adding animal to cage > " + getAllAnimals() );  
}
```
addAnimal() 에서 `Cage<? super T>`는 **T** 또는 **T의 상위 타입**을 담을 수 있는 Cage 임을 의미한다.<br>
여기서 `? super T` 를 사용하는 것은 반공변성을 이용한 것이다. T 의 상위 타입을 다룰 수 있다는 말은 즉, 이 문맥 안에서 **최소 T 타입은 안전하게 다룰 수 있다**는 뜻이다. 

addAnimal을 사용해보자
```java
Cage<Carnivore> cCage = new Cage<>(); // -> Cage 클래스의 T 타입을 Carnivore로 지정  
cCage.addAnimal( cCage, new Tiger() ); // OK. 
cCage.addAnimal( cCage, new Lion() );  // OK.
```
cCage 인스턴스는 Carnivore 타입을 담는 Cage 객체이다. <br>
이 때 Cage 클래스 입장에서는 addAnimal( cCage, new Tiger() ) 이 호출될 때,
-  첫번째 매개변수 `Cage<? super T> cage` : 실제 인자로 `Cage<Carnivore>` 타입이 넘어왔으니 문제가 없다.
- 두번째 매개변수 `T animal` :  실제 인자로 Tiger 타입과 Lion 타입이 넘어왔다. animals 는 `List<Carnivore>`이므로 Carnivore의 하위 타입인 Tiger와 Lion은 안전하게 들어갈 수 있다.

```java
List<Carnivore> carnivoreList = new ArrayList<>();  
carnivoreList.add( new Tiger() ); // OK
```


## 와일드카드`?` 를 활용한 변성
위의 내용을 정리하자면, 제네릭 타입은 기본적으로 `불공변`이지만 **와일드카드의 경계를 설정**함으로써 `공변` 또는 `반공변`을 적용하도록 컴파일러에 트릭을 줄 수 있다.

| 경계      | 표현식          | 변성   | 설명                                       |
| --------- | --------------- | ------ | ------------------------------------------ |
| 상한 경계 | `<? extends T>` | 공변 적용   | 상위 클래스 제한 (T와 그 자식 타입만 가능) |
| 하한 경계 | `<? super T>`   | 반공변 적용 | 하위 클래스 제한 (T와 그 조상 타입만 가능) | 


### 와일드카드 경계에 따른 동작 제약
List 자료형으로 살펴보자
#### `<? extends T>`
- 값 조회 : T 타입으로 받아야 안전하다.
- 값 저장 : 불가

- 제네릭으로 받은 값을 꺼내는 경우
```java
public class AnimalSample {  
    public static void method( List<? extends Animal> animal ){  
        Animal animal1 = animal.get( 0 ); // 안전함  
        
        /* 안전 X */        
        Tiger animal2 = (Tiger)animal.get( 0 ); // Tiger의 상위 타입이 오거나 Lion 타입이 오면 런타임시 ClassCastException 발생    
        Lion animal3 = (Lion)animal.get( 0 ); // Lion의 상위 타입이 오거나 Tiger 타입이 오면 런타임시 ClassCastException 발생  
    }  
  
    public static void main( String[] args ) {  
        List<Animal> animals = new ArrayList<>(  
            Arrays.asList( new Animal(), new Animal(), new Animal() )  
        );  
        List<Lion> lions = new ArrayList<>(  
            Arrays.asList( new Lion(), new Lion(), new Lion() )  
        );  
  
        method( animals );  
        method( lions );  
    }  
}
```

- 제네릭으로 받은 값에 특정 값을 저장하는 경우
```java
public static void setMethod( List<? extends Animal> animal ) {  
    // 저장 X  
    animal.add(new Animal()); // 컴파일 에러!
    animal.add(new Carnivore()); // 컴파일 에러!
    animal.add(new Tiger()); // 컴파일 에러!
    animal.add(new Lion()); // 컴파일 에러!

	// 저장 O -> null
    animal.add(null); // null 만 삽입 가능  
}
```
가장 상위인 `List<Animal>` 타입이 온다면 문제가 없겠지만 실제로 어떤 자식 타입이 또 들어올지 컴파일러 입장에서는 모르기 때문에 그냥 불가하도록 처리한다.
➔ 인자에 값을 넣고 싶다면 `super` 와일드카드를 사용해야 한다.


### `<? super T>`
- 값 조회 : Object 타입으로 받아야 안전하다
- 값 저장 : **T와 그 자식 타입만** 넣을 수 있다.
이 부분이 개인적으로 가장 헷갈렸다. 코드로 살펴보자

- 제네릭으로 받은 값을 꺼내는 경우
```java
public class AnimalSample {  
    public static void getMethod( List<? super Carnivore> animal ){  
        Object animal0 = animal.get( 0 ); // 안전함  
  
        /* 안전 X */        
        Animal animal1 = (Animal) animal.get( 0 );  
        Carnivore animal2 = (Carnivore) animal.get( 0 );  
        Tiger animal3 = (Tiger) animal.get( 0 );  
        Lion animal4 = (Lion) animal.get( 0 );  
    }  
  
    public static void main( String[] args ) {  
        List<Animal> animals = new ArrayList<>();  
        animals.add( new Animal() );  
        animals.add( new Carnivore() );  
        animals.add( new Tiger() );  
  
  
        getMethod( animals );  
    }  
}
```

getMethod() 내에서 animal의 값을 꺼낼 때 **Object**로 받아야 안전하다. 
그 이유는 getMethod()가 파라미터로 Carnivore의 상위 타입을 받을 수 있도록 설정했기 때문에 animal은 Carnivore, Animal, Object 타입이 올 수 있기 때문이다.

이 메소드를 호출하는 곳에서 Carnivore 타입보다 더 상위 타입의 리스트를 보낸다면, getMethod() 내부에서 더 작은 타입으로 형변환을 시도할 때 **ClassCastException**이 발생한다.
예를 들어 `List<Animal>`를 인자로 호출한다면, getMethod() 내부에서 값을 Carnivore 타입으로 형변환을 할 때 ( `animal2` ) 에러가 발생한다.
따라서 어떤 상위의 값이 들어와도 안전하게 꺼낼 수 있도록 `Object` 타입으로 받아야 한다.

- 제네릭으로 받은 값을 저장하는 경우
```java
public static void setMethod( List<? super Carnivore> animal ){  
    // 저장 -> 본인과 그 자식만 가능  
    animal.add( new Carnivore() );   
    animal.add( new Tiger() );   
    animal.add( new Lion() );   
      
    animal.add( new Animal() ); // 컴파일 에러!  
    animal.add( new Object() ); // 컴파일 에러!  
}
```

만약 인자로 `List<Carnivore>` 타입이 넘어온다면 animal에 `new Animal()` 을 추가할 수 없다. Carnivore 타입의 리스트는 요소로 Animal 타입을 담을 수 없기 때문이다.
따라서 어떤 타입이 와도 안전하게 저장하기 위해서는 `super` 로 최소 타입이 보장된 Carnivore 타입이 업캐스팅 가능한 상한선이 된다.


## 느낀점
<figure>
  <img width="589" alt="image" src="https://github.com/grey920/grey920.github.io/assets/58028215/bc0d0975-01b7-4913-a647-5652ee711414">
  <figcaption>Wildcard subtyping in Java can be visualized as a cube</figcaption>
</figure>


...
<figure>
  <img src="https://static.hubzum.zumst.com/hubzum/2019/03/05/11/b4e02040204e4f17aef43b13a8d7ec30.jpg" width="450">
  <figcaption>뫼비우스..의 띠..?</figcaption>
</figure>

처음엔 보고 이게 뭐지...? 싶었다. <br>
정말 계속 보고 계속 쳐보고 챗지피티 괴롭히고 난리 부르스를 치니 조금 느낌이 온다.. <br>
그래도 반공변 개념은 여전히 계속 헷갈려서 앉았을땐 알았다가 의자에서 일어서면 까먹는다.. ㅎ <br>
마음으로 잘 받아들여지지 않는 것 같다.. 왜.. 왜.. 반대로 가는건데...!! <br>
일단 제네릭 타입 수준에서 다운캐스팅을 하려는 것이다,, 라고 외우련다🫠
<br>


## 출처(참고문헌)
- [Covariance and contravariance (computer science)](https://en.wikipedia.org/wiki/Covariance_and_contravariance_(computer_science)#Inheritance_in_object-oriented_languages)
- [자바 제네릭의 공변성 & 와일드카드 완벽 이해](https://inpa.tistory.com/entry/JAVA-%E2%98%95-%EC%A0%9C%EB%84%A4%EB%A6%AD-%EC%99%80%EC%9D%BC%EB%93%9C-%EC%B9%B4%EB%93%9C-extends-super-T-%EC%99%84%EB%B2%BD-%EC%9D%B4%ED%95%B4)
- [프로그래밍 초식](https://www.youtube.com/watch?v=PtM44sO-A6g)
- [Covariance, Contravariance, and Invariance — What do they mean?](https://medium.com/@bendaniel10/covariance-contravariance-and-invariance-what-do-they-mean-part-1-351f7865b506)

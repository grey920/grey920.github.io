---
title: "[Typescript] 타입"
excerpt: ""
categories:
  - Client
tags:
  - Typescript
toc: true
toc_sticky: true
toc_label: 목차
toc_icon: "list"
# header:
  # teaser: /assets/images/2022-04-03/after.png
---
> tl;dr
* 선택적 타입을 다루려면: ? (optional 타입)
* Alias 타입 생성: type 타입명 (시작은 대문자)
* 함수의 인자 타입: 파라미터 괄호 안에 인자명**:타입**
* 함수의 리턴 타입: 함수명(인자)**: 리턴타입** {}
* readonly: 읽기 전용으로 수정할 수 없는 상태
* readonly tuple: 아무것도 변경할 수 없는 상태
* any: typescript의 보호장치를 완전히 비활성화시킴
> 

## 타입 시스템 ( 타입을 정하는 방법 )

타입스크립트는 모든 것의 타입을 정해주어야 한다 (type checker와 소통하는 방식)

Typescript는 두가지 접근 방식을 결합했다.

1. 데이터와 변수의 타입을 명시적으로 정의하거나
2. 일반 자바스크립트처럼 변수만 생성하고 넘어가거나 (타입스크립트가 타입을 추론)

> 타입스크립트의 Type checker가 타입을 추론하도록 하는 것이 더 좋다.
 -> 코드가 더 짧고 가독성이 좋기 때문에!
* 명시적 방법이 더 유용한 경우? -> Typescript가 타입을 추론하지 못할 때
> 

### Implicit Type

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled.png" | relative_url }}' width="600" />
</figure>

타입 스크립트가 변수 a를 알아서 string 타입으로 추론한다

### Explicit Type

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%201.png" | relative_url }}' width="600" />
</figure>

타입스크립트에게 명시적으로 알려준다.

### 추론/명시적 방법 - 예시1

1) 추론을 사용한 방법

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%202.png" | relative_url }}' width="600" />
</figure>

2) 명시적으로 선언하는 방법

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%203.png" | relative_url }}' width="600" />
</figure>

## 타입스크립트의 타입

### 기본 타입

문법 - 뒤에 **`: 타입`** 을 붙인다

- number
- string
- boolean

배열의 경우 타입 뒤에 []를 붙인다.

```tsx
let a: number[] = [1, 2, 3];
let b: string[] = ["a", "b", "c"];
let c: boolean[] = [true]
-------------------------------
// 추론하게 두는 것이 더 낫다
let a = [1,2];
let b = ["a", "b", "c"];
let c = [true, false]
```

### optional 타입

만약 아래의 player 객체가 있을 때, player들 중 몇몇은 age가 있고 몇몇은 age가 없지만 모두 name을 가지고 있다면 어떻게 type checker에게 알려줄 수 있을까?

```tsx
const player = {
    name: "grey"
}
```

object의 타입을 정의해준다. ? 를 붙이면 선택적으로 들어올 수 있다는 뜻이다.

```tsx
const player**: {**
    name: string,
    **age?: number**
**}** = {
    name: "grey"
}
```

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%204.png" | relative_url }}' width="600" />
</figure>

optional로 명시하니 age 변수에 타입으로 numer 또는 undefined 타입이 올 수 있다고 나온다.

age를 number타입과 비교 연산을 하면 다음과 같이 에러가 발생한다.

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%205.png" | relative_url }}' width="600" />
</figure>

undefined가 될 수도 있다는 에러를 발생하는데  이는 player.age가 존재하는지 확인을 거쳐야 한다는 뜻이다.

따라서 player.age가 undefined가 아님을 확인시켜줘야 한다

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%206.png" | relative_url }}' width="600" />
</figure>

### Alias 타입 생성

같은 타입을 여러번 지정해줘야 하는 경우 이런 식으로 계속 반복하는것은 좋지 않다.

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%207.png" | relative_url }}' width="600" />
</figure>

이런 경우 Alias 타입 (별칭)을 생성할 수 있다.

- 첫 글자는 대문자로 작성한다

Player라는 타입으로 별칭을 만들어 적용하면 다음과 같다

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%208.png" | relative_url }}' width="600" />
</figure>

이러면 많은 타입을 **재사용**할 수 있게 된다.

Player 타입 안에 있는 age 역시 Alias로 만들 수 있다. 

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%209.png" | relative_url }}' width="600" />
</figure>

> [타입을 구축하기 위한 두 가지 구문](https://typescript-kr.github.io/pages/tutorials/ts-for-js-programmers.html)
1. interface
2. type
interface를 우선적으로 사용하고 특정 기능이 필요할 때 type을 사용해야 한다
> 

### 함수 타입

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2010.png" | relative_url }}' width="600" />
</figure>

playerMaker 함수는 타입이 string인 name을 가진 object를 반환한다

하지만, Player 타입을 리턴하고 싶다면 함수의 파라미터 괄호 뒤에 리턴할 `:타입` 을 붙여준다

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2011.png" | relative_url }}' width="600" />
</figure>


이러면 string 타입으로 name을 받고 Player 타입을 return 하는 함수가 된다

화살표 함수로 만드는 것도 동일하다

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2012.png" | relative_url }}' width="600" />
</figure>


## 타입에 readonly 속성 추가하기 (불변성 부여하기)

자바스크립트에는 없지만 타입스크립트에는 이 읽기 전용 동작을 구현하고 싶다면 쓸 수 있는 보호장치가 있다.

readonly 속성을 추가하면 readonly가 적용된 속성을 수정하려고 할 때 타입스크립트가 이를 멈춘다.

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2013.png" | relative_url }}' width="600" />
</figure>


number 배열을 readonly 속성으로 지정한 경우 역시 push를 쓸 수 없다. 

push가 readonly number[] 타입에 존재하지 않기 때문이다

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2014.png" | relative_url }}' width="600" />
</figure>


하지만 map이나 filter같은 경우 array를 직접 바꾸지 않기 때문에 사용할 수 있다

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2015.png" | relative_url }}' width="600" />
</figure>

### Tuple

최소한의 길이를 가지고 특정 위치에 특정 타입이 있는 array를 생성

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2016.png" | relative_url }}' width="600" />
</figure>


이를 사용하면 항상 정해진 갯수(3개)의 요소를 순서에 맞는 타입으로 가져와야 하는 array를 지정할 수 있다.

지정하지 않은 경우 첫번째 인덱스에 number형을 넣어도 에러가 없다

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2017.png" | relative_url }}' width="600" />
</figure>


하지만 tuple로 생성하면 첫번째 인덱스에 string이 와야 한다고 에러를 뱉는다

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2018.png" | relative_url }}' width="600" />
</figure>


tuple과 readonly를 합치면 아무것도 바꿀 수 없는 상태가 된다

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2019.png" | relative_url }}' width="600" />
</figure>


### undefined, null

undefined와 null은 자바스크립트에도 있는 타입이다.

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2020.png" | relative_url }}' width="600" />
</figure>


선택적 타입(optional)은 undefined가 될 수 있다

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2021.png" | relative_url }}' width="600" />
</figure>

### any

비어있는 값들을 쓰면 기본값이 any이다.

예를 들어, 빈 array를 만들면 타입스크립트는 기본적으로 any의 array라고 생각한다

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2022.png" | relative_url }}' width="600" />
</figure>

any는 타입스크립트로부터 빠져나오고 싶을 때 쓰는 타입이다. (보호장치들로부터 빠져나와 타입스크립트에게 바보같은 짓을 하고 싶다고 허락받고 싶다면 사용한다?!)

그렇기 때문에 타입스크립트를 사용한다면 any를 사용하지 않는 것을 권장한다.

예를 들어 다음의 코드는 any를 썼을 때엔 문제가 없는 코드이다.

( number배열과 boolean이 + 연산을 할 수 있다)

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2023.png" | relative_url }}' width="600" />
</figure>

둘 중 하나인 b만 any로 한다고 해도 무리없이 동작한다

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2024.png" | relative_url }}' width="600" />
</figure>

하지만 타입스크립트로 쓴다면 바로 에러를 내뱉는다

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2025.png" | relative_url }}' width="600" />
</figure>

아무데서나 any를 쓸 수 없도록 몇가지 규칙을 타입스크립트 설정으로 추가할 수 있다. 

## 타입스크립트에만 존재하는 타입

어떤 타입인지 모르는 변수는 Typescript에게 어떻게 말해줘야 할까?

예를 들어 API로부터 응답을 받는데 그 응답의 타입을 모르는 경우 -> unknown이라는 타입을 쓸 수 있다.

### unknown

변수의 타입을 미리 알지 못할 때 unknown을 사용한다.

변수에 타입을 unknown으로 설정하면 타입스크립트로부터 일종의 보호를 받게 된다.

- 일종의 보호? → 어떤 작업을 하려면 이 변수의 타입을 먼저 확인해야 한다

예를 들어 unknown으로 지정한 변수 a와 1을 더하는 연산을 하는 경우 에러가 발생한다

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2026.png" | relative_url }}' width="600" />
</figure>

여기서 에러를 피하려면 a가 number인지 확인하는 코드를 작성해야 한다

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2027.png" | relative_url }}' width="600" />
</figure>

typeof로 number임을 확인하는 if문 안에 연산을 작성하면 해당 블록 내에서 a는 number 타입이기 때문에 + 연산이 가능하게 된다

이렇게 타입을 확인한다면 toUpperCase()도 사용할 수 있다.

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2028.png" | relative_url }}' width="600" />
</figure>

### void

void는 아무것도 return하지 않는 함수를 대상으로 사용한다.

타입스크립트에서 함수가 아무것도 리턴하지 않는 것을 자동으로 인식하기 때문에 보통 void를 따로 지정해줄 필요는 없다.

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2029.png" | relative_url }}' width="600" />
</figure>

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2030.png" | relative_url }}' width="600" />
</figure>

contextual typing(문맥상의 타이핑)에서 void 타입 반환은 함수가 **아무것도 반환하지 않음을 강제하지 않는다** 

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2031.png" | relative_url }}' width="600" />
</figure>

참고로 변수에는 오직 undefined만 할당할 수 있다.

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2032.png" | relative_url }}' width="600" />
</figure>

### never

함수가 절대 return하지 않을 때 발생한다. (함수가 절대 끝까지 실행되지 않는 경우)

예를 들어 함수에서 리턴하지 않고 exception(예외)가 발생하는 경우라고 할 수 있다

리턴 타입이 never인 함수에서 return 값을 “X”라고 하면 지정할 수 없다는 에러가 뜬다

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2033.png" | relative_url }}' width="600" />
</figure>

하지만 함수 안에서 에러를 던져주면 정상적으로 넘어간다

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2034.png" | relative_url }}' width="600" />
</figure>

또한 타입이 두가지일수도 있는 상황에서 발생할 수도 있다

<figure>
  <img src='{{ "/assets/images/2022-05-23/Untitled%2035.png" | relative_url }}' width="600" />
</figure>

타입 체크로 두 가지 타입을 모두 확인한 후에는 마지막 name에 뭘 쓰던 그 타입은 never가 된다. 이 말은 즉 저 마지막 else문은 절대 실행되지 않아야 한다는 뜻이다.
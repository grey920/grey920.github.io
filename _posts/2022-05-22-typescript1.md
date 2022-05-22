---
title: "타입스크립트의 동작 원리"
excerpt: "자바스크립트도 어려운데 타입스크립트 꼭 써야하나요? 넹 (단호)"
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
<!-- ## tl;dr -->

## 1. 타입스크립트, <span class="custom-color">어떻게</span> 생긴 언어인가

### strongly typed programming language

- 자바와 같이 컴파일을 통해 기계가 실행할 수 있는 다른 종류의 코드로 변환되는 언어
- 타입스크립트는 작성한 코드가 자바스크립트로 변환된다
    - 왜 변환해야 하는가?
        - **브라우저가 `자바스크립트`를 이해**하기 때문에!
        - Node.js는 타입스크립트와 자바스크립트 둘 다 이해할 수 있다

## 2. 타입스크립트, 어떻게 동작하는가

불안정한 자바 스크립트를 컴파일할 뿐인데 어떻게 개발자가 이상한 코드를 작성하는것으로부터 보호할 수 있는걸까?

### 보호장치

- 타입스크립트가 자바스크립트로 변환되기 전에 발행한다
- 타입스크립트가 먼저 코드를 확인한 후 변환된 자바스크립트 안에서 실수가 일어나지 않도록 확인해준다
- 타입스크립트 코드에 에러가 발생할 것 같은 코드가 감지되면, 코드는 자바스크립트로 컴파일되지 않는다.
- 즉, 타입스크립트가 정상적으로 자바스크립트로 컴파일되었다면 이는 자바스크립트 코드에 버그가 전혀 없다는 뜻이다.

### 예시

1. 객체 내 존재하지 않는 함수 호출
    <figure>
      <img src='{{ "/assets/images/2022-05-22/typescript/Untitled.png" | relative_url }}' width="600" />
    </figure>
    자바스크립트에서는 객체 내의 존재하지 않는 함수를 호출하는 경우에 실행시에 에러가 발생하지만 코드 작성시에는 에러가 발생하지 않았다. 
    
    하지만 타입스크립트에서는 코드를 저장하기 전에 바로 존재하지 않는 속성이라는 에러 메시지를 던져주고 있다.
    

1. 다른 타입의 연산
  <figure>
    <img src='{{ "/assets/images/2022-05-22/typescript/Untitled%201.png" | relative_url }}' width="600" />
  </figure>
    
2. 함수의 인자가 다른 경우
  <figure>
    <img src='{{ "/assets/images/2022-05-22/typescript/Untitled%202.png" | relative_url }}' width="600" />
  </figure>
    

### 보호장치가 생기는 이유? → 타입추론 때문

- 타입추론이란?
    - 타입스크립트가 코드를 해석해 나가는 동작을 의미한다
- 타입추론의 과정
    - 변수를 선언하거나 초기화 할 때 타입이 추론된다.
        
        ```tsx
        let x = 3;
        ```
        
    - 이외에도 변수, 속성, 인자의 기본값, 함수의 반환값 등을 설정할 때 타입 추론이 일어난다

### 타입 추론 방식

1. 가장 적절한 타입 (Best Common Type)
    - 보통 몇 개의 표현식(코드)을 바탕으로 가장 근접한 타입을 추론한다
        
        ```tsx
        let arr = [0, 1, null];
        ```
        
    - 위의 경우 변수 arr의 타입을 추론하기 위해서는 배열의 각 아이템을 살펴봐야 한다.
        - 크게 number와 null로 구분된다.
    - 이 때 Best Common Type 알고리즘으로 다른 타입들과 가장 잘 호환되는 타입을 선정한다.
2. 문맥상의 타이핑 (Contextual Typing)
    - 코드의 위치(문맥)을 기준으로 타입을 결정한다.
    - 예를 들어,
        
        ```tsx
        window.onmousedown = function(mouseEvent){
        	console.log(mouseEvent.button); // OK
        	console.log(mouseEvent.kangaroo); // Error!
        }
        ```
        
        1. 타입스크립트 검사기는 `window.onmousedown` 에 할당되는 함수의 타입을 추론하기 위해 `window.onmousedown` 의 타입을 검사한다
        2. 타입 검사가 끝나면 함수의 타입이 마우스 이벤트와 연관이 있다고 추론하기 때문에 `mouseEvent` 인자에 `button` 속성은 있지만 `kangaroo` 속성은 없다고 결론을 내린다



### 타입스크립트의 타입 체킹

- 타입스크립트의 지향점은 타입 체크는 값의 형태에 기반하여 이루어져야 한다는 점이다 → 덕 타이핑 (Duck Typing) 또는 Structural Subtyping이라고 한다
    - [Duck Typing](https://www.notion.so/duck-typing-8941285ea9454ae88c940e70aa5fa6a4) : 객체의 변수 및 메서드의 집합이 객체의 타입을 결정한다. 동적 타이핑의 한 종류
    - Structural Subtyping: 객체의 실제 구조나 정의에 따라 타입을 결정한다

## 3. 타입스크립트, <span class="custom-color">왜</span> 써야 하는가

### 자바스크립트의 단점

1. 실수를 피할 수 없다.
    - 다른 타입끼리의 연산이 가능하다
        
        ```jsx
        [] + true // -> 실행이 됨!! 
        ```
        
    - 함수 실행시 올바른 입력값을 사용하도록 강제하지 않는다
      <figure>
        <img src='{{ "/assets/images/2022-05-22/typescript/Untitled%203.png" | relative_url }}' width="600" />
      </figure>
        
    - 객체 안에 존재하지 않는 함수를 호출할 수도 있다. 코드가 실행되고 나서야 에러 메시지를 볼 수 있다. (작성시에는 알 수 없다 => **`런타임 에러`** 는 실제 유저가 만나게 될 에러이기에 매우 안좋다)
      <figure>
        <img src='{{ "/assets/images/2022-05-22/typescript/Untitled%204.png" | relative_url }}' width="600" />
      </figure>
        
    
    즉, 코드를 실행하기 **전에** 이러한 에러를 잡아내고 싶다는 필요성이 생겼다
    

1. 코드 가이드 및 자동완성으로 개발 생산성 향상
    - VS code 툴의 내부가 타입스크립트고 작성되어 있어 타입스크립트 개발에 최적화 되어있다.
    - 자바스크립트의 경우 코드를 작성할 때 total이라는 변수의 타입이 어떤 타입인지를 알 수 없기 때문에 number의 API를 사용할 수 없다(sum함수의 리턴값이 any이다. 즉 number로 확정되지 않은 상태)
      <figure>
        <img src='{{ "/assets/images/2022-05-22/typescript/Untitled%205.png" | relative_url }}' width="600" />
      </figure>
        
        
    - 타입스크립트의 경우 변수 total에 대한 타입이 지정되어 있기 때문에 해당 타입에 대한 API를 미리보기로 띄워줄 수 있어 더 빠르고 정확하게 코드를 작성할 수 있다.
     <figure>
        <img src='{{ "/assets/images/2022-05-22/typescript/Untitled%206.png" | relative_url }}' width="600" />
      </figure>
        
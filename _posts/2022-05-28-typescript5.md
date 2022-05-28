---
title: "[Typescript] 함수 - 다형성"
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
## 다형성이란?
- 프로그래밍 언어에서 다형성이란, 여러 타입을 받아들임으로써 여러 형태를 가지는 것을 의미한다.

## 배열의 요소를 출력하는 예제

### call signature를 일일이 만들어서 쓰는 경우

call signature로 경우의 수를 하나하나씩 만들어 줄 수 있지만 다양한 타입을 다 작성하는 것은 모든 가능성을 다 조합해야 하기 때문에 좋지 못하다.

⇒ 이럴때 generic을 사용하면 된다

<figure>
  <img src='{{ "/assets/images/2022-05-28/Untitled.png" | relative_url }}' width="600" />
</figure>

## Generic

- Generic이란? → placeholder같은 것 (?!). 타입이 들어올 것을 알지만 concrete 타입이 아니다.
- 내가 요구하는 대로 signature를 생성해주는 도구라고 생각하자
- generic을 언제 사용할까
    - call signature를 작성할 때 들어올 확실한 타입을 모르는 경우 사용한다.

### 제네릭 사용하는 법

1. 먼저 타입스크립트에게 generic을 사용하고 싶다고 알려주어야 한다. (in call signature)
    
    ```tsx
    type SuperPrint = {
        **<TypePlaceHolder>(**arr: **TypePlaceHolder**[]): void
    }
    ```
    
    **`<>`** 이 꺽쇠를 쓰면 generic을 쓰는 것이다. 이 안에 어떤 것을 넣어도 상관없지만 <T>나 <T, V>를 많이 보게 될 것이다.
    
    꺽쇠안에 TypePlaceHolder라고 지정하고 arr의 파라미터 타입을 똑같이 지정해준다
    
2. call signature 안에서 generic을 사용하면 함수를 호출하는 부분에서 전달하는 값을 보고 타입스크립트가 추론해서 들어온 값으로 TypePlaceHolder를 대체한다.
  <figure>
    <img src='{{ "/assets/images/2022-05-28/Untitled%201.png" | relative_url }}' width="600" />
  </figure>
    

*리턴값을 변경한 경우에도 똑같이 적용할 수 있다. 예를 들어 배열의 첫번째 요소를 반환한다고 한다면 call signature의 리턴 타입에도 TypePlaceHolder를 설정한다. 이렇게 하면 타입스크립트가 리턴값 역시 추론해서 해당 값으로 TypePlaceHolder를 대체한다.
<figure>
  <img src='{{ "/assets/images/2022-05-28/Untitled%202.png" | relative_url }}' width="600" />
</figure>


만약 제네릭을 추가하고 싶다면 

1. <>꺽쇠 안에 이름을 하나 더 지정해준다.
2. 어디에서 쓸 지를 지정해준다 (ex. 두번째 파라미터에서 M을 쓸 것이다) 
3. 이러면 타입스크립트는 제네릭이 처음 사용되는 지점을 기반으로 이 타입이 무엇인지를 알게된다.
<figure>
  <img src='{{ "/assets/images/2022-05-28/Untitled%203.png" | relative_url }}' width="600" />
</figure>

대부분의 경우 이제 각각의 변수의 타입을 지정해 줄 필요없이 제네릭으로 선언해줘도 된다.

> 참고로 any와 generic은 다르다. <br>
> any를 쓰는 경우 타입스크립트의 보호장치를 완전히 해제하는 것이고 generic은 다양한 타입을 받을 수 있도록 타입스크립트가 추론해서 알맞게 대체되는 것이다.
> 

### 제네릭을 사용하는 경우

- 제네릭을 사용해 타입을 생성할 수도 있고, 어떤 경우에는 타입을 확장할 수도 있다. 어떤 경우에는 타입을 저장하기도 한다.
- 많은 것들이 있는 큰 타입(Player) 안에 하나가 달라질 수 있는 요소(extraInfo)라면 그것을 generic으로 넣는다 ⇒ 재사용성이 높아짐
<figure>
  <img src='{{ "/assets/images/2022-05-28/Untitled%204.png" | relative_url }}' width="600" />
</figure>
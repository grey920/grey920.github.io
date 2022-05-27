---
title: "[Typescript] 함수 - 오버로딩"
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

## 오버로딩 (overloading)

fucntion overloading이나 method overloading이라고도 불린다.

우리가 사용할 외부 라이브러리나 패키지들은 오버로딩을 많이 사용하기 때문에 우리가 직접 오버로딩을 구현할 일이 많지 않다고 하더라도 어떻게 생긴 놈인지 익혀 두어야 한다.

### call signature의 예시

우리가 3.에서 배운 call signature의 모습

```tsx
type Add = (a: number, b: number) => number; 
```

이 모양은 사실 짧게 표현한 것이고, 더 풀어서 쓸 수도 있다.

```tsx
type Add = {
	(a: number, b: number): number; 
}
```

이게 가능한 이유는 바로 오버로딩 때문이다.

### 오버로딩이란?

오버로딩은 함수가 서로 다른 여러개의 call signature를 가지고 있을 때 발생시킨다.

### 1) 타입이 다른 argument를 가질 때

예를들어 Router를 사용해서 페이지를 바꾸고 싶을 때

```tsx
// stirng 타입을 보내는 경우
Router.push("/home")
--------------------------
// 객체 형식으로 보내는 경우
Router.push({
	path: "/home",
	state: 1
})
```

이 두 가지가 모두 잘 작동한다 
  <figure>
    <img src='{{ "/assets/images/2022-05-27/Untitled.png" | relative_url }}' width="600" />
  </figure>

어떤 파라미터를 받을 때 어떤 동작을 하는지 이렇게 작성하는 것으로 보통 라이브러리나 패키지를 디자인할 때 많이 사용하게 된다.

### 2) 다른 여러개의 argument를 가질 때

만약 call signature1은 하나의 파라미터를 가지지만 call signature2는 세 개의 파라미터를 받는 경우라면? 

type Add의 예시로 돌아가서 살펴보자.

number 타입의 파라미터 2 개를 받는 call signature와 number 타입의 파라미터 3 개를 받는 call signature를 type Add로 작성했다면, add 함수를 구현할 때 파라미터로 넘어간 c는 옵션이다. 

다시 말하자면, type Add는 a, b를 가지고 c가 들어올 수도 있고 안들어올 수도 있다.

따라서 파라미터의 갯수가 다르다면, 나머지 파라미터도 타입을 지정해줘야 한다.

<figure>
  <img src='{{ "/assets/images/2022-05-27/Untitled%201.png" | relative_url }}' width="600" />
</figure>

c는 선택사항이라는 것을 `?: 타입` 으로 알려주면 넘어가게 된다.

<figure>
  <img src='{{ "/assets/images/2022-05-27/Untitled%202.png" | relative_url }}' width="600" />
</figure>


이러면 파라미터 갯수가 다른 add(1, 2)와 add(1, 2, 3) 모두 잘 동작한다.

### overloading signature

<figure>
  <img src='{{ "/assets/images/2022-05-27/Untitled%203.png" | relative_url }}' width="600" />
</figure>


참고: [A Simple Explanation of Function Overloading in TypeScript](https://dmitripavlutin.com/typescript-function-overloading/)
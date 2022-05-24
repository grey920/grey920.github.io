---
title: "[Typescript] 함수 - call signature"
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

1) 함수 선언 첫번째 방법
  <figure>
    <img src='{{ "/assets/images/2022-05-24/Untitled.png" | relative_url }}' width="600" />
  </figure>

  - 리턴타입을 항상 명시해야 하는 것은 아니다. 알아서 리턴 타입을 추론해서 넘어간다

2) 화살표 함수
  <figure>
    <img src='{{ "/assets/images/2022-05-24/Untitled%201.png" | relative_url }}' width="600" />
  </figure>
   

## 호출 시그니쳐(call signatures)

call signatures란 함수 이름 위에 커서를 올렸을 때 뜨는 파라미터 타입 정보와 리턴 타입 정보를 말한다. <br>
<span class="custom-color">함수를 어떻게 호출</span>해야 하는지와 <span class="custom-color">반환이 어떻게 되는지</span> 알려주는 정보

### 나만의 call signature를 선언하는 방법

call signature로 개발자가 직접 타입을 만들 수 있고, 함수가 어떻게 동작하는지 서술해둘 수 있다

```tsx
type Add = (a: number, b:number) => number;
```

위에처럼 작성하면 이제 타입스크립트에게 타입이 number라고 말해줄 필요가 없다
<figure>
  <img src='{{ "/assets/images/2022-05-24/Untitled%202.png" | relative_url }}' width="600" />
</figure>

장점1. 먼저 함수의 타입을 설명하고 나서 코드를 구현하게 되기 때문에, 개발자가 타입을 생각하도록 해준다.

함수 파라미터 안에서 직접 타입을 설정할 때엔 코드 구현과 동시에 타입을 지정했지만, call signature를 쓰면 타입 지정과 함수 구현을 분리해서 작성할 수 있다.
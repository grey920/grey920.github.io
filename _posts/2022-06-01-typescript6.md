---
title: "[Typescript] Class"
categories:
- Client
tags:
- Typescript
toc: true
toc_sticky: true
toc_label: 목차
toc_icon: list
---

## 타입스크립트에서 Class 만드는 법


> 💡  자바스크립트와 다른 점
> 
> - constructor()에서 this.프로퍼티로 작성하던 부분을 안해도 된다.
> - constructor 내부에 접근제어자와 타입을 명시하면 된다
> - 명시해놓은 접근제어자는 javascript로 컴파일되면 보이지 않는다.


### 생성자 함수 및 private 키워드
<figure>
  <img src='{{ "/assets/images/2022-06-01/typescript/Untitled.png" | relative_url }}' width="600" />
</figure>


- 다른 점
    - javascript에서는 this.프로퍼티 로 생성자 함수에서 속성을 넣어주었다면, typescript에서는 그럴 필요가 없다.
    - javascript로 컴파일될 때에는 private 접근자가 사라졌다. private 키워드는 타입스크립트가 우리를 보호해주기 위해서만 사용되는 것이기 때문. 자바스크립트에서는 private 키워드가 사용되지 않는다.

    <figure>
    <img src='{{ "/assets/images/2022-06-01/typescript/Untitled%201.png" | relative_url }}' width="600" />
    </figure>

    <figure>
    <img src='{{ "/assets/images/2022-06-01/typescript/Untitled%202.png" | relative_url }}' width="600" />
    </figure>

    - private 속성을 바로 쓸려고 하면 타입스크립트에서는 이렇게 에러가 뜬다. (자바스크립트는 가능함)
    - public 속성인 nickName만 접근 가능하다.

### 추상클래스 (abstract Class)

> 추상클래스란?
>    - 다른 클래스가 상속받을 수 있는 클래스
>    - 추상 클래스는 새로운 인스턴스를 직접 생성할 수 없다. (new 사용 X)

<figure>
<img src='{{ "/assets/images/2022-06-01/typescript/Untitled%203.png" | relative_url }}' width="600" />
</figure>

- Player에 있던 constructor를 추상클래스인 User 내부로 옮겨주었다.
- Player 클래스는 User 클래스를 extends 키워드로 상속받는다.

<figure>
  <img src='{{ "/assets/images/2022-06-01/typescript/Untitled%204.png" | relative_url }}' width="600" />
</figure>

- 추상클래스는 인스턴스를 직접 생성할 수 없다.

### 추상 클래스 내의 메서드와 추상메서드 (abstract method)

> 추상메서드란?
>   - 추상 클래스를 상속받는 모든 것들이 구현해야 하는 메소드
>   - 추상 클래스 내에서는 구현하지 않는다.
>   - 즉, 구현 방법은 상관없지만 구현을 하기를 원할 때 사용한다

[추상 클래스 내 메서드] 

- 예시로 추상클래스인 User 안에 getFullName()이라는 메서드를 작성했다
<figure>
  <img src='{{ "/assets/images/2022-06-01/typescript/Untitled%205.png" | relative_url }}' width="600" />
</figure>

- grey 인스턴스는 Player 클래스가 User 클래스를 상속받았기 때문에 User 클래스의 getFullName() 메소드를 사용할 수 있다.
<figure>
  <img src='{{ "/assets/images/2022-06-01/typescript/Untitled%206.png" | relative_url }}' width="600" />
</figure>

- User 클래스 내 메소드에 private 키워드를 사용하면 이 역시 외부에서 사용할 수 없게된다.

[추상클래스]
<figure>
  <img src='{{ "/assets/images/2022-06-01/typescript/Untitled%207.png" | relative_url }}' width="600" />
</figure>

- abstract getNickName(): void 이렇게 call signature만 명시한다
<figure>
  <img src='{{ "/assets/images/2022-06-01/typescript/Untitled%208.png" | relative_url }}' width="600" />
</figure>

- User 클래스를 상속받는 Player 클래스에서는 추상메서드인 getNickName()을 무조건 구현해야 하기 때문에 타입스크립트에서 에러를 출력하고 있다.






Player 클래스에서 getNickName()을 구현해보자.


<figure>
  <img src='{{ "/assets/images/2022-06-01/typescript/Untitled%209.png" | relative_url }}' width="600" />
</figure>

- 여기서 this 키워드로 콘솔 로그를 찍으면 에러가 난다. 추상메서드 내에서 private 카워드로 property를 지정했기 때문이다.
- private 키워드를 사용하면 자식 클래스에서도 사용할 수 없다. 만약 자식 클래스에서 사용하길 원한다면 대신 protected 키워드를 사용하자.
<figure>
  <img src='{{ "/assets/images/2022-06-01/typescript/Untitled%2010.png" | relative_url }}' width="600" />
</figure>

부모 클래스인 User의 프로퍼티 접근자를 protected로 변경했기 때문에 이제 자식 클래스인 Player 내에서 this.nickName으로 프로퍼티에 접근할 수 있게 되었다.

### dictionary 예제

```tsx
type Words = {

    // object의 타입을 선언해야할 때 사용할 수 있다.
    // 이 object는 제한된 양의 property를 가질 수 있고, 이 property에 대해 이름을 알지 못하지만 타입만 알고있을 때 쓸 수 있다 
    [key: string]: string
}

class Dict {
    private words :Words

    // 수동으로 생성자를 초기화한다 
    constructor(){
        this.words = {}
    }

    // 단어를 추가한다
    // 파라미터가 Word 클래스의 인스턴스이기 원하기 때문에 Word 타입을 받도록 지정한다 
    add( word: Word ){
        // 주어진 사전에 아직 단어가 없는 경우
        if ( this.words[word.term] === undefined ) {
            this.words[word.term] = word.def;
        }
    }

    // term 으로 단어를 조회한다
    def( term: string ){
        return this.words[term];
    }
}

class Word {
    constructor(
        public term: string,
        public def: string
    ){}
}

const kimchi = new Word("kimchi", "한국의 음식");

const dict = new Dict();
dict.add( kimchi );
dict.def( "kimchi" );
```

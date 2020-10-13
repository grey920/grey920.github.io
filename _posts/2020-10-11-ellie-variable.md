---
title: "[드림코딩 엘리] 자바스크립트3. 데이터 타입"
excerpt: 엘리의 자바스크립트 강의 정리 (변수와 데이터 타입)
categories:
    - javascript
tags:
    - javascript
    - ellie
toc: true
toc_sticky: true
# toc_label: ArrayList
---

-   프로그래밍 언어에서 가장 중요한 것은??
    -   **입력, 연산, 출력**!
    -   **CPU에 최적화된 연산**과 **메모리의 사용을 최소화** 하는 것도 중요하다

# Variable (변수)

### 시작 환경

index.html

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>Document</title>
		<script src="variable.js"></script>
	</head>
	<body></body>
</html>
```

variable.js

```jsx
// 1. Use strict
// added in ES 5
// use this for Vanila Javascript
"use strict";

```

-   바닐라 자바스크립트로 프로그래밍 할 때에는 파일 제일 위에 'use strict' → 모던하게 사용 가능

### 변수

-   Variable 변수 : 변경될 수 있는 값
-   **let** : JS에서 변수 만들 때 쓰는 키워드. ES6에 추가됨 (현대적인 것들은 ES6에서 추가되었다)

variable.js

```jsx
// 2. Variable 변수:  변경될 수 있는 값
// let (added in ES6)

let name = "ellie";
console.log(name);
name = "hello";
console.log(name);
```

-   name이라는 변수를 선언함과 동시에 ellie라는 값을 할당
-   다시 name 변수에 hello라는 값을 할당

어플리케이션을 실행하면 메모리가 할당된다.
let이라는 키워드로 변수를 정의하면, 메모리를 가리키는 포인터가 생성됨
name이라는 변수가 가리키는 메모리 어딘가에 ellie라는 값을 저장할 수 있다.

### Block scope

-   코드를 블럭안에 작성하면, 블럭 밖에서는 안의 내용을 볼 수 없다

```jsx
// 2. Variable 변수:  변경될 수 있는 값
// let (added in ES6)
{
	let name = "ellie";
	console.log(name);
	name = "hello";
	console.log(name);
}
console.log(name); // 블럭 밖 -> 아무 값도 출력되지 않는다
```

<!-- ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f26a316b-04b6-458a-8763-e3d6e29cea31/_2020-10-11__7.56.13.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f26a316b-04b6-458a-8763-e3d6e29cea31/_2020-10-11__7.56.13.png) -->

-   global scope : 블럭을 쓰지 않고 파일 안에 바로 정의해서 쓰는 변수 (전역변수)
-   어디서나 접근이 가능하다.
-   글로벌한 변수들은 애플리케이션 실행 순간부터 끝날 때까지 항상 메모리에 탑재된다 ⇒ **최소한으로** 쓰는 것이 좋다.
    -   가능하면 class나 함수, if, for 등 필요한 부분에서만 정의해서 쓰는 것이 좋다 .

```jsx
let globalName = "global name";
{
	let name = "ellie";
	console.log(name);
	name = "hello";
	console.log(name);
	console.log(globalName);
}
console.log(name); // 블럭 안 변수 - 콘솔에 출력 x
console.log(globalName); // 글로벌 변수 - 콘솔에 출력 o
```

<!-- ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a8d01397-2ee4-4d4c-9df4-03dd11f83aaf/_2020-10-11__8.11.50.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a8d01397-2ee4-4d4c-9df4-03dd11f83aaf/_2020-10-11__8.11.50.png) -->

### let

-   자바스크립트에서 변수를 선언할 수 있는 키워드.
-   그 이전에는?? → var (쓰지마!!)

    -   왜??
    -   1. var는 선언하기도 전에 값을 줄 수도, 값을 넣기 전에 출력하는 일도 가능하다 ⇒ var hoisting

        -   var hoisting : 어디에 선언했냐에 상관없이 항상 제일 위로 선언을 끌어 올려주는 것

        ```jsx
        // var (don't ever use this!!!!)
        console.log(age);
        age = 4;
        console.log(age);
        var age;
        ```

        콘솔

        <!-- ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/35adeb33-7476-4d23-bff7-d33f486ddb99/_2020-10-11__8.21.06.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/35adeb33-7476-4d23-bff7-d33f486ddb99/_2020-10-11__8.21.06.png) -->

        ```jsx
        // let을 쓴다면??
        name = 4;
        let name;
        ```

        <!-- ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/55eb43e4-f4a4-448b-a520-e98db3df6c43/_2020-10-11__8.23.08.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/55eb43e4-f4a4-448b-a520-e98db3df6c43/_2020-10-11__8.23.08.png) -->

        -   변수를 선언하기도 전에 접근했다는 에러메시지가 출력됨 ⇒ 정상

    -   2. var는 블록 스코프가 없다. 즉, 블럭을 철저히 무시한다

        ```jsx
        // var (don't ever use this!!!!)
        // var hoisting (move declarationfrom bottom to top)
        // has no block scope
        {
        	age = 4;
        	var age;
        }
        console.log(age);
        ```

        <!-- ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fb5b039d-5a36-4bd1-82a5-500583c14c4c/_2020-10-11__8.32.09.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fb5b039d-5a36-4bd1-82a5-500583c14c4c/_2020-10-11__8.32.09.png) -->

        -   블럭 안에서 변수를 선언 했음에도 밖에서 출력할 때 정상적으로 출력된다
        -   아무리 깊은 곳에 변수를 선언 해도 아무 곳에서 호출할 때 출력이 된다. → 규모가 있는 프로젝트를 하다보면, 선언하지 않은 값이 할당되는 이상한 일들이 일어난다.

### Constants

-   한 번 할당하면 값이 절대 변하지 않는 값
-   가리키는 포인터가 잠겨 있어서 값을 선언함과 동시에 할당한 뒤로는 절대 값을 변경할 수 없다.
-   이유
    -   보안상의 이유 : 해커들이 다른 코드로 바꾸는 것을 방지
    -   thread safety
        -   어플리케이션이 실행되면 한 가지 프로세스가 할당되고, 그 프로세스 안에서 다양한 쓰레드가 동시에 돌아가면서 어플리케이션이 효율적으로 동작하도록 돕는다.
        -   다양한 쓰레드들이 동시에 변수에 접근해서 값을 변경할 수 있다(→ 위험함)
        -   이를 방지하기 위해 값이 변하지 않는 상수로 막는다.
    -   코드 변경 시 실수를 방지

```jsx
// 3. Contants
// favor immutable data type always for a few reasons :
//  - security
//  - thread safety
//  - reduce human mistakes
const daysInWeek = 7;
const maxNumber = 5;
```

---

즉, JS에서는 변수를 선언할 때
Mutable 타입의 **let**과 Immutable 타입의 **const** 이렇게 두 가지가 있다

### Variable Types

-   primitive type : 더 이상 작은 단위로 나눠질 수 없는 한 가지 아이템
    -   number, string, boolean, null, undefined, symbol
-   Object : 싱글 아이템들을 여러 개 묶어서 한 박스로 관리할 수 있게 함
    -   function, first-class function

```jsx
// 4. Variable Types
// 1) primitive type  2) Objective type
// primitive, single item : Number, string, boolean, null, undefined, symbol
// Object, box container
// function, first-class function
const count = 17; // integer
const size = 17.1; // decimal number (소숫점 숫자)
console.log(`value: ${count}, type: ${typeof count}`);
console.log(`value: ${size}, type: ${typeof size}`);
```

<!-- ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/37e8bf0a-2f80-48b8-b805-31884980560b/_2020-10-11__8.58.26.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/37e8bf0a-2f80-48b8-b805-31884980560b/_2020-10-11__8.58.26.png) -->

-   정수와 소수 상관없이 type은 number이다.

### number

```jsx
// number - special numeric values: infinity, -infinity, NaN
const infinity = 1 / 0;
const negativeInfinity = -1 / 0;
const nAn = "not a number" / 2;
console.log(infinity);
console.log(negativeInfinity);
console.log(nAn);
```

<!-- ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ca8b5368-0f11-42cd-851d-9c20eea05ea7/_2020-10-11__9.02.52.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ca8b5368-0f11-42cd-851d-9c20eea05ea7/_2020-10-11__9.02.52.png) -->

-   infinity : 양수를 0으로 나눌 때
-   -infinity : 음수를 0 으로 나눌 때
-   NaN : 숫자가 아닌 string 타입을 숫자로 나눌 때

> 연산할 때 항상 그 값이 유효한 값인지 확인하고 연산해야 한다

### string

-   한 개든, 여러개든 상관없이 string이다.

```jsx
// string
const char = "c";
const brendan = "brendan";
const greeting = "hello " + brendan;
console.log(`value: ${greeting}, type: ${typeof greeting}`);
const helloBob = `hi ${brendan}!`; // template literals
console.log(`value: ${helloBob}, type: ${typeof helloBob}`);
```

<!-- ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/91fb6142-eefe-4c3e-8fc1-8648ab6a7d2f/_2020-10-11__9.11.40.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/91fb6142-eefe-4c3e-8fc1-8648ab6a7d2f/_2020-10-11__9.11.40.png) -->

-   template literals (string) : 백틱기호(``)를 이용해서 원하는 string을 적고 달러 싸인과 기호를 이용하면 ( \${} ) 변수에 값이 자동으로 붙여져서 나온다.

    console.log(`value: ${greeting}, type: ${typeof greeting}`);

### boolean

-   참과 거짓

```jsx
// boolean
// false : 0, null, undefined, NaN, ''
// true : any other value
const canRead = true;
const test = 3 < 1; // false
console.log(`value: ${canRead}, type: ${typeof canRead}`);
console.log(`value: ${test}, type: ${typeof test}`);
```

<!-- ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c928f941-ef35-48a9-8414-30e1472e59c2/_2020-10-11__9.18.33.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c928f941-ef35-48a9-8414-30e1472e59c2/_2020-10-11__9.18.33.png) -->

### null과 undefined

-   null : 명확하게 null 즉, 텅 빈 값인 empty값이라고 지정함.
-   undefined : 선언은 되었지만 아무 값도 지정되어 있지 않음 (텅 비어있는지 값이 있는지 정해지지 않은 상태)

```jsx
// null
let nothing = null;
console.log(`value: ${nothing}, type: ${typeof nothing}`);

//undefined
let x;
console.log(`value: ${x}, type: ${typeof x}`);
```

<!-- ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5b801ebd-b100-4640-b5a5-fcf80ce7c18e/_2020-10-11__9.21.16.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5b801ebd-b100-4640-b5a5-fcf80ce7c18e/_2020-10-11__9.21.16.png) -->

### symbol

-   나중에 map이나 다른 자료구조에서 고유한 식별자가 필요하거나, 동시다발적으로 일어날 수 있는 상황에서 우선순위를 주고 싶을 때 정말 고유한 식별자를 주고 싶을 때 사용.

```jsx
// symbol, create unique identifiers for objects
const symbol1 = Symbol("id");
const symbol2 = Symbol("id");
console.log(symbol1 === symbol2); // 동일한지 확인
```

<!-- ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/83f3428f-8e91-4e73-addb-ddcfe132d942/_2020-10-11__9.28.29.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/83f3428f-8e91-4e73-addb-ddcfe132d942/_2020-10-11__9.28.29.png) -->

-   false가 출력됨.
-   동일한 string 값(id)이 들어가도 다르게 인식됨.
-   string이 똑같을 때 동일한 symbol값을 주고 싶다면??

    -   Symbol.for()를 이용

        ```jsx
        // symbol, create unique identifiers for objects
        const symbol1 = Symbol("id");
        const symbol2 = Symbol("id");
        console.log(symbol1 === symbol2); // 동일한지 확인

        const gSymbol1 = Symbol.for("id"); // 주어진 스트링에 맞는 심볼을 만들어라
        const gSymbol2 = Symbol.for("id");
        console.log(gSymbol1 === gSymbol2); // true
        ```

        <!-- ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/42c91e57-40dc-4985-9ec4-d5a0246adfb7/_2020-10-11__9.32.22.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/42c91e57-40dc-4985-9ec4-d5a0246adfb7/_2020-10-11__9.32.22.png) -->

-   symbol은 바로 출력하면 에러가 나온다

    ```jsx
    console.log(`value: ${symbol1}, type: ${typeof symbol1}`);
    // Uncaught TypeError: Cannot convert a Symbol value to a string
    ```

    -   .description을 이용해서 string으로 변환 후 출력해야 한다

### object

-   일상생활에서 보는 물체들을 대표할 수 있는 박스 형태.

```jsx
// object, real-life object, data structure
const ellie = { name: "ellie", age: 20 };
ellie.age = 21;
```

-   ellie는 const로 지정되어 있기 때문에 메모리의 포인터가 잠겨있어서 다른 오브젝트로 할당이 불가하지만, ellie 오브젝트 안에 있는 name, age 변수들은 ellie.name, ellie.age로 다른 값을 할당해줄 수 있다.
<!--
    <img src="https://s3-us-west-2.amazonaws.com/secure.notion-static.com/07ea545f-93a0-4b32-a161-2b97f2ae665a/_2020-10-11__9.55.44.png"> -->

### Dynamic typing

-   c나 자바같은 언어는 statically typed language. → 변수를 선언할 때 어떤 타입인지 결정해서 타입을 같이 선언한다.
-   자바스크립트는 선언할때 어떤 타입인지 선언하지 않고 런타임(프로그램이 동작할 때) 할당된 값에 따라서 타입이 변경될 수 있다. (dynamically typed language)
-   이런 언어는 좋은 아이디어가 있을 때 빠르게 프로토타입을 할 수 있다는 장점
-   규모가 있는 프로젝트에서는 단점일 수 있다.
-   예시

        ```jsx
        // 5. Dynamic typing : dynamically typed language
        let text = "hello";
        console.log(`value: ${text}, type: ${typeof text}`); // string
        text = 1;
        console.log(`value: ${text}, type: ${typeof text}`); // number
        text = "7" + 5;
        console.log(`value: ${text}, type: ${typeof text}`); // string (string + string)
        text = "8" / "2";
        console.log(`value: ${text}, type: ${typeof text}`); // number
        ```

        <!-- <img src="https://s3-us-west-2.amazonaws.com/secure.notion-static.com/92e39d5a-acda-4a91-9a2b-4717bca22dbe/_2020-10-11__9.45.21.png"> -->

        -   런타임시 타입이 지정되기 때문에 런타임 에러가 생길 수 있다

        ```jsx
        let text = "hello";
        console.log(text.charAt(0)); //h
        console.log(`value: ${text}, type: ${typeof text}`);
        text = 1;
        console.log(`value: ${text}, type: ${typeof text}`);
        text = "7" + 5;
        console.log(`value: ${text}, type: ${typeof text}`);
        text = "8" / "2";
        console.log(`value: ${text}, type: ${typeof text}`);
        console.log(text.charAt(0)); //Uncaught TypeError: text.charAt is not a function
        ```

    <!-->

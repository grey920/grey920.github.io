---
title: "서브라임 텍스트(Sublime Text) 매크로 사용하기"
excerpt: "개발자라면 단순반복적인 일은 하기 싫자나여?"
categories:
  - Tip
tags:
  - Sublime Text
  - Macro
  - 매크로
toc: true
toc_sticky: true
toc_label: 목차
toc_icon: "list"
# header:
  # teaser: /assets/images/2022-04-03/after.png
---
## tl;dr
> 1. 매크로 녹화 시작: control + Q (종료도 단축키 동일)
> 2. 반복하고자 하는 행동 수행
> 3. 매크로 종료
> 4. 매크로 실행: control + shift + Q


## 사건의 발단,,
며칠 전 쿼리 작성 중 90개가 넘는 컬럼의 alias를 camel case로 다 맞춰주어야 하는 작업을 해야했다. (아찔,,) <br>
다섯개쯤 바꾸고 있자니 이거는 도저히 일일히 할 수 없는 상황임을 느꼈고,,<br>
예전 사수님이 Visual Studio에서 매크로를 돌려서 이런 반복작업을 빠르게 처리했던 것이 생각났다. <br>
마침 맥에서 쓸 에디터를 찾고있던 차에 서브라임 테스트가 매크로가 된다기에 다운받고 바로 실행해보았다.

## 기대 동작
1. 문장 끝으로 이동 후 컬럼명 블록만 선택 후 복사 -> AS 쓰고 붙여넣기
2. 붙여넣은 snake 케이스를 camel 케이스로 변경 (case convert 플러그인 사용)
  - [참고 블로그](https://reference-m1.tistory.com/362)
3. 쉼표, 찍고 아래 문장의 끝으로 이동

## 매크로 사용하기
-  [Tools] > Record Macro 선택 : 녹화 시작
  <figure>
    <img src='{{ "/assets/images/2022-05-15/macro1.png" | relative_url }}' width="600" />
    <figcaption> 단축키 control + Q </figcaption>
  </figure>
-  원하는 동작 수행 (종료 전까지 사용자의 행동이 기록됨)
  <figure>
    <img src='{{ "/assets/images/2022-05-15/macro2.png" | relative_url }}' width="600" />
    <figcaption> 위의 기대 동작을 수행 </figcaption>
  </figure>
-  [Tools] > Stop Recording Macro : 녹화 종료
  <figure>
    <img src='{{ "/assets/images/2022-05-15/macro3.png" | relative_url }}' width="600" />
    <figcaption>녹화 시작과 같은 단축키 control + Q </figcaption>
  </figure>
-  [Tools] > Playback Macro : 녹화 실행
  <figure>
    <img src='{{ "/assets/images/2022-05-15/macro.gif" | relative_url }}' width="600" />
    <figcaption> 단축키 control + shift + Q</figcaption>
  </figure>



---
## 참고
[Macro · 서브라임 텍스트3 사용자 가이드 - jeonghak](https://jeonghakhur.gitbooks.io/sublime-text3/content/macro.html)
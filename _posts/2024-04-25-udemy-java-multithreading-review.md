---
title: "[유데미] Java 멀티스레딩, 병행성 및 성능 최적화 - 전문가 되기 후기"
excerpt: ""
categories:
  - Review
tags:
  - Udemy
  - Java
  - 성능최적화
  - 멀티스레딩
toc: true
toc_sticky: true
toc_label: "목차"
toc_icon: "edit"
# classes: wide
header:
  teaser: "/assets/images/글또_유데미.png" #/assets/images/2022-01-02/Untitled.png
---

## 서론

Java 언어로 개발을 한지 벌써 3년이 넘었다.. 세상에<br>
지난 시간을 돌아보니 요구사항에 맞춰 애플리케이션 코드를 구현할 순 있으나 그 이상 성능 최적화를 실무에 적용한 적은 없었던 것 같아 아쉬움이 들었다. JDK 21 에서 가상 스레드를 공식 feature로 제공하는데 이에 대한 내용을 잘 몰라 불안한(?) 느낌도 있었다. <br>
그리고 특히 비전공자로서 CS 지식이 부족하다는 생각을 가지고 있었기 때문에 운영체제 관련된 이야기만 나오면 나는 늘 긴장하기 일쑤였다.<br>

그러던 차에 마침 글또 x 유데미 협찬으로 Java 성능 최적화 강의가 있어 해당 강의를 듣게 되었다.
<figure>
  <img src='https://github.com/grey920/grey920.github.io/assets/58028215/e342df2c-dabb-4ddf-a6d6-3a8afba931ad'>
  <figcaption></figcaption>
</figure>


## 강의에서 다루는 내용
해당 강의는 총 5.5시간 강의이다. (나는 정리하면서 학습하다보니 일주일이나 걸렸다..ㅎ)
<figure>
  <img src='https://github.com/grey920/grey920.github.io/assets/58028215/37947a5f-22db-414d-80cc-e251ecf7b1a0' width='80%'>
  <figcaption></figcaption>
</figure>

해당 강의는 Java를 사용하는 개발자가 애플리케이션을 개발할 때 어떻게 지연 시간, 처리량 등 성능을 높일 수 있을지 관련 개념을 설명하고 직접 코드를 작성하는 형태로 진행한다. <br>
이를 위해 Java의 관련 클래스와 메서드를 무작정 외우는 게 아니라, 어떤 개념을 왜 알아야 하는지 그 당위성을 알려주고, 관련된 시스템의 작동 방법을 친절하게 알려준다. 

아래는 각 섹션에서 나오는 개념들이 어떻게 유기적으로 연결되는지 보여주기 위해 필기의 일부분이다.<br>
가장 첫 세션에서 OS가 어떤 일을 하고, 프로세스와 스레드가 어떻게 구성되는지, 그리고 스케줄링이 어떤 기준에 의해 동작하는지 등을 알려준다. 이러한 배경 설명을 먼저 듣고 나서, 실질적으로 어떻게 Java 코드를 통해 성능을 향상시킬 수 있는지를 배우기 때문에 더 이해가 쏙쏙 되는듯 하다.
<figure>
  <img src='https://github.com/grey920/grey920.github.io/assets/58028215/c336e4ac-7fd8-4b74-ac02-e96ed716592f' >
  <figcaption></figcaption>
</figure>



## 좋았던 점
### 다양한 그림 설명과 친절한 예시
강의에서 가장 자주 나오는 개념이 OS와 Thread에 관한 내용이다. 코드나 하드웨어처럼 눈에 보이지 않다보니 동작 방법을 글로만 접하게되면 완전히 이해되는 것이 아니라 피상적으로 문장만 외워지는 느낌이었다. <br>
하지만 강의에서는 추상적으로 개념을 그림으로 그려주고, 작업 프로세스는 도표로 시각화해서 더 직접적으로 이해가 되었다.

<figure>
  <img src='https://github.com/grey920/grey920.github.io/assets/58028215/9d7236c4-2d3f-46f7-9e0e-b3628657b596' >
  <figcaption></figcaption>
</figure>


### 실습 코드 제공
강의에서는 이론 설명 뿐만 아니라 간단한 코드를 직접 타이핑하며 보여준다. 코드를 보며 따라쳐도 좋지만, 시간이 너무 오래 걸려서 제공해주는 예제 코드를 다운받아 실행해보고, 한 줄씩 주석을 달아가며 공부했다.<br>
가끔씩 어떤 강의들은 제공해주는 예제가 작동하지 않거나 설정이 어려워 실행하는데 어려움을 겪곤 했는데 해당 강의는 간단하고 핵심적인 예제만 제공해서 무리없이 실행할 수 있었다.
<figure>
  <img src='https://github.com/grey920/grey920.github.io/assets/58028215/2883fe97-aaae-4650-8a7d-a98e1dd9b4b3' >
  <figcaption></figcaption>
</figure>

<figure>
  <img src='https://github.com/grey920/grey920.github.io/assets/58028215/f0e2844b-e06e-41c6-bae9-b7f342e9d131' >
  <figcaption></figcaption>
</figure>



### 내용 정리 퀴즈와 구현 과제
이 강의에서 가장 좋았던 점은 한 섹션이 끝날 때마다 배운 내용을 확인하는 퀴즈가 2~3개씩 있어서 적극적으로 복습할 수 있었다는 점이다. <br>
수업을 들을땐 모든게 당연하고 다 이해가 되는 것처럼 느껴진다. 모든게 머릿속에 들어있는 것 같지만 막상 문제를 풀어보면 낯설게 느껴지고 어떤 부분이 어려운지 바로 알게된다.

<figure>
  <img src='https://github.com/grey920/grey920.github.io/assets/58028215/9161659b-648c-4337-9f53-282c356a5383' >
  <figcaption></figcaption>
</figure>

퀴즈를 풀면 틀린 문제를 확인할 수 있다. 근데 틀린 문제에 대한 해설이 자세하진 않아서 해설만 온전히 믿을 순 없다. 직접 따로 구글링하자.

<figure>
  <img src='https://github.com/grey920/grey920.github.io/assets/58028215/cf132197-dc56-472b-b815-3420730292a4' >
  <figcaption></figcaption>
</figure>

퀴즈 외에도 5개의 코딩 연습 문제가 있다. 퀴즈보다는 확실히 직접 손으로 타이핑을 쳐야 제대로 학습이 되는것 같다. <br>
문제는 큰 에러가 나지 않으면 그냥 성공으로 넘어가는 것 같은 느낌이 있긴 하지만 다음 페이지에 코딩 연습에 대한 해설이 있어서 문제를 제대로 파악했는지 확인할 순 있다. 

<figure>
  <img src='https://github.com/grey920/grey920.github.io/assets/58028215/67297dd2-b064-4083-84d8-2dcb21c9a2b9' >
  <figcaption></figcaption>
</figure>


## 아쉬운 점
### 영어의 장벽
한글 자막이 제공되긴 하지만 그래도 영어 강의에 대한 낯설음은 어쩔 수 없는 것 같다. <br>
귀로는 영어가 들리고 눈으로는 한글을 보니 머릿속에서 멀티태스킹이 일어나는 느낌이다.<br>
그래도 한글 자막이 없어 눈치로 때려 맞추고 코드만으로 공부하던 것과 비교하면 너무나 좋아진 환경이니까..!!<br>
인터넷 강의의 좋은 점이 언제든 일시정지를 할 수 있다는 점이니 속도에 욕심부리지 않고 차근히 학습하면 무리는 없을걸로 보인다. 

### 강의 질문
개인적으로 강의를 볼 때 다른 사람들이 올린 질문을 많이 보는 편이다. 다른 사람들의 질문을 보면서 내가 생각치 못했던 포인트들을 발견할때도 많아 생각의 확장이 이루어지는 경우가 많기 때문이다. <br>
이 강의만 그런진 모르겠으나 해당 강의는 전체 질문이 8개 밖에 없어서 개인적으로 아쉬웠다.

<figure>
  <img src='https://github.com/grey920/grey920.github.io/assets/58028215/25c3df57-672e-4883-aaec-158ba3770bcc' >
  <figcaption></figcaption>
</figure>


## 추천하는 사람
- 어느정도 자바를 다루어봤고, 성능에 대한 고민을 시작한 사람
- 자바 애플리케이션의 성능 향상을 실무에서 도입하기 전 가볍게 관련 개념을 익히고 싶은 사람
- OS와 자바 애플리케이션의 상호작용에 대해 좀 더 알고싶은 사람

## 결론
사실 백그라운드가 전혀 없는 사람이 이 강의만 듣고 바로 실무에서 성능 향상을 이루어내겠다! 는 무리가 있을 것 같다. 관련된 키워드와 간단한 개념 및 특징을 찍먹하는 정도의 깊이로 다루기 때문이다. <br>
하지만 스스로 예제를 만들어보며 학습하고, 강의에 나온 키워드만이라도 공부를 잘 해둔다면 큰 도움이 될 것같다.



<br>
<br>
<figure>
  <img src='/assets/images/글또_유데미.png' width="550">
  <figcaption>해당 콘텐츠는 유데미로부터 강의 쿠폰을 제공받아 작성되었습니다.</figcaption>
</figure>

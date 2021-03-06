---
title: "프로그래밍 잘하고 싶다면 코드는 '이렇게' 짜세요"
excerpt: "초보개발자 개발 스킬업 1편"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Devlog
tags:
 - tip
toc: true
toc_sticky: true
toc_label: 목차
description: 좋은 코드와 좋은 코드를 짜기 위해 어디에 집중해야 하는지 알아보기 
---

출처 : [삼평동연구소](https://youtu.be/N7jcUb2T4RA)

## 1. 프로그래밍 공부

> 좋은 코딩 습관을 갖추는 것에 집중하자

주석이 아닌 코드로 설명되는 명확한 코드를 짜는 것을 목표로 한다.

- 정확한 함수나 변수의 네이밍
- 명확한 인터페이스
- 불필요한 최적화 코드는 최대한 사용하지 말자
    - 잘못 쓰면 오히려 **가독성**이 떨어진다.
- 주석이 꼭 필요한 곳, 반드시 필요한 곳에 주석 달기 
⇒  나를 포함해 다른 사람이 이해하기 훨씬 수월함.
    - 나 혼자 쓰는 것이 아닌 **인터페이스에** 해당하는 **함수**
    - 성능을 위해 최적화를 했지만 가독성이 떨어지는 **함수**
    - **장애**가 발생했었던 코드들 (히스토리가 있는 코드들)

예시)

### 함수

- 함수가 명확한 기능을 하는가
- 함수에 전달되는 파라미터의 선택
- 파라미터의 올바른 IN/OUT 설정
- 함수의 명확한 return
- 함수가 적절한 기능 단위로 잘 분리되어 있는가 - open read write close
- 쌍이 맞는가 - 예) insert()가 있는데 delete()가 없을 경우

## 2. 언어의 특징 알아두기

> 효율적 구현을 위해 언어의 특징을 알아두자

예)

- "str1" == "str2"  vs  StringCompare("str1", "str2")

결과는 같다 ⇒ '**차이점**은 뭘까?' 생각하기 → 메모리 할당 / 성능 등

- 숫자 증감에서 i++ / ++i 의 차이를 알고서 사용하는가?
- 동적배열 → 초기에 기본 배열값은 얼마가 좋을까?
- Hashtable, List, 동적배열, Map ...

언어마다 내부적으로 구현된 알고리즘이 다를 수 있다. 그에 따라 성능도 달라지기 때문에 중급으로 레벨업 하기 위해서는 잘 알아두는게 중요하다!! 

## 추천팁!
1. 책과 블로그 등에서 지식을 쌓아가자 : 이펙티브00같은 책 (이펙티브 자바..)
2. 비슷한 기능을 하는 몇 가지가 있을 때 **항상 의문을 갖고** 고민하자
3. 언어에 추가되는 신기능을 알아두자 ⇒ 불필요한 코드량을 줄이는 등의 생산성 향상 기대
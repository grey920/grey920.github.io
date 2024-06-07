---
title: "[항해99 취업 리부트 코스 학습일지][day3] 프로젝트 핵심만 빠르게 분석하는 꿀팁"
excerpt: ""
categories:
  - TIL
tags:
  - 개발자포트폴리오
  - 개발자이력서
  - 개발자취업
  - 개발자취준
  - 코딩테스트
  - 항해99
  - 취리코
  - 취업리부트코스
toc: true
toc_sticky: true
toc_label: "목차"
toc_icon: "edit"
# classes: wide
header:
  teaser: /assets/images/hanghae99-teaser.png
---

## 새로 배운 내용
### 프로젝트 복기 템플릿
첫 날에도 느꼈듯 ( [첫 날 후기](https://grey920.github.io/til/hanghae99-day1-til/#%EC%9D%B4%EB%A0%A5%EC%84%9C-%EA%B3%BC%EA%B1%B0%EC%9D%98-%EB%82%98%EC%99%80-%EC%A1%B0%EC%9A%B0%ED%95%98%EB%8A%94-%EC%88%9C%EA%B0%84) ), 특히나 저처럼 이직을 준비하시는 분이라면 준비 과정 중 가장 어려운 점이 바로 **지난 프로젝트 내용 복기** 일 것입니다. <br>
저의 경우, 프로젝트 명과 어떤 기능을 개발했는지는 기록을 잘 적어두었지만
- 그 기능을 왜 만들어야했는지
- 기능을 구현하면서 기술적으로 어떤 고민/문제가 있었는지
- 그 방법을 선택한 이유는 무엇인지, 다른 방법은 없었는지

등 스쳐간 수많은 생각들은 코드 구현하는 시간에 밀려 제대로 작성해두질 않았습니다. 기록이 없는 기억은 금새 휘발되더군뇨.. 생각보다 너무 빨리.. 흑흑

기억 속에서 길 잃은 어린 양을 위해 천사같은 구름 매니저님이 꿀같은 `프로젝트 복기 템플릿`을 알려주셨습니다.

#### 📌 템플릿 작성 순서
1. 주어진 질문을 먼저 확인합니다.
2. 각 질문에 맞는 코드를 프로젝트에서 찾고, 코드를 채워 넣습니다.
3. 어떤 방식/ 의도를 가지고 코드가 구성되어 있는지 천천히 살펴봅니다.
4. 설명에 대한 내용을 채워 나갑니다.
<br>

#### 📌 템플릿
- 어떤 핵심을 가진 프로젝트인가요?
  - 핵심 기능의 코드 작성
  - 기능에 대해 간단한 설명
- 해당 기능을 구현한 로직에 대해 설명해 주세요. (인자, 동작 방식, 리턴값 등)
- Service에서 사용한 모든 어노테이션의 설명을 어노테이션과 함께 적어주세요. (기능X, 사용 의도와 목적)
- ERD를 구성/설계할 때, 발생했던 문제는 무엇인가요? 그리고 해당 구조로 데이터셋을 다시 구성한다면 어떻게 해볼 수 있을까요?
- 더욱 더 최적화된 방법과 설계를 시도한다면, 어떻게 할 수 있을까요?
  - 간단한 구조 설명과 함께 코드 작성
- 성능 최적화 (쿼리 최적화, 인덱싱, 캐싱 처리 등) 또는 동시성 제어를 반영한 코드가 있다면 코드와 함께 설명해주세요
  - 코드 작성
  - 어떤 프로세스로 작동하는지 설명
<br>



#### 📌 프로젝트 복기 템플릿, 좋았던 점
- 프로젝트의 `핵심`에 대해서만 집중적으로 고민할 수 있게되어 좋았습니다. 
  - 특히 프로젝트의 핵심 기능의 코드를 찾아보고 해당 기능에 대해 간단히 설명하면서 자연스럽게 '면접관님이 이 프로젝트에 대해 물어보시면 이런 식으로 답을 해야겠다!' 라는 식으로 머릿속에서 면접 시뮬레이션이 그려졌습니다.
- 프로젝트를 `객관적`으로 바라볼 수 있어서 좋았습니다.
  - 개발을 하다보면 내가 맡은 파트만 보게되는 경향이 있는데, 템플릿의 질문을 따라가다보니 내가 맡지 않은 부분이라도 프로젝트에서 중요하고 알아야 하는 부분들을 찾게 되었습니다. 이해하려고 노력하다보니 프로젝트에 대한 전반적인 이해도가 더 높아졌습니다:)
- 이력서를 작성하면서 프로젝트의 성능에 관한 고민없이 기능 구현에만 시간을 쓴 것 같아서 고민이었는데 템플릿을 작성하면서 늦게나마 어떻게 하면 더 나은 방식으로 `개선`할 수 있을지 고민하게 되어 마음이 후련하고 좋았습니다.


> **🔍 더 공부하고 싶은 키워드**
> - @Async 비동기 처리와 동시성 



<br>
<br>
항해99 취업 리부트 코스를 수강하고 작성한 콘텐츠 입니다. <br>
<a>https://hanghae99.spartacodingclub.kr/reboot</a>
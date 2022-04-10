---
title: " Nuxt에서 Vuex 스토어 사용하기"
excerpt: "프로젝트에 선적용, 후학습하여 정리하는 내용..ㅎ"
categories:
  - Client
tags:
  - Nuxt
  - Vue
  - Vuex
  - Store
toc: true
toc_sticky: true
toc_label: 목차
toc_icon: "list"
# header:
  # teaser: /assets/images/2022-04-03/after.png
---

## Vuex 스토어?

[모든 페이지들에서 자유롭게 읽고 쓸 수 있는 저장소가 스토어이고 이를 관리 해주는 Vue.js의 라이브러리 중 하나가 Vuex이다.](https://velog.io/@nuxt/Nuxt.js-VuexStore)

Vue에서 데이터를 주고받기 위해서 보통 부모-자식 컴포넌트끼리 props / 이벤트 emit으로 전달할 수 있지만, 나의 경우 다른 페이지로 화면을 전환하면서 다량의 데이터를 함께 전달해야했기 때문에 이벤트버스나 쿼리스트링으로 넘기기엔 한계가 있어서 모든 컴포넌트에 대한 중앙 집중식 저장소 역할을 하는 스토어를 사용하게 되었다.  

### Vuex의 데이터 전달 흐름

![https://media.vlpt.us/images/nuxt/post/5a20a4bb-e3de-43fa-82a3-446f79a77dc1/vuex.png](https://media.vlpt.us/images/nuxt/post/5a20a4bb-e3de-43fa-82a3-446f79a77dc1/vuex.png)

데이터의 흐름은 Actions → Mutations → State 순서이다.

- State: 여러 컴포넌트 간에 공유되는 데이터
- Mutations: 뷰엑스에서 state 값을 변경하는 유일한 방법(setter같다고 생각하면 될 듯). 동기처리 담당.
- Actions: 뮤테이션 중에서 비동기 처리 로직들을 정의. API호출이나 데이터 가공이 주로 일어난다.
- getters: computed 속성과 매칭되는 기술 요소. state값이 변경되었을때 변화에 따른 차이를 자동으로 반영하여 값을 계산한다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbwQByt%2FbtqAlQpvCcZ%2F4EOdCgiZ6KtdVjtTemhjbk%2Fimg.png" width="550"/>

사용자가 뭔가 액션을 취했을 때 Actions는 Mutations에 commit을 통해 State를 변경한다. State의 값이 변경이 되면 해당하는 컴포넌트가 다시 로딩된다.  

## Store 활성화

Nuxt 기본 설정이 비활성화로 되어 있기 때문에 활성화를 시켜주어야 한다.

## 참고

- [****Nuxt.js에서 Vuex(Store) 사용 하기](****[https://velog.io/@nuxt/Nuxt.js-VuexStore](https://velog.io/@nuxt/Nuxt.js-VuexStore))
- [Nuxt 공식 홈페이지] ([https://nuxtjs.org/docs/directory-structure/store](https://nuxtjs.org/docs/directory-structure/store))
- [https://velog.io/@nuxt/Vuex-명명-규칙](https://velog.io/@nuxt/Vuex-%EB%AA%85%EB%AA%85-%EA%B7%9C%EC%B9%99)
- [****Vuex in Nuxt] (****[https://joshua1988.github.io/vue-camp/nuxt/store.html](https://joshua1988.github.io/vue-camp/nuxt/store.html))
- [****상태 관리 소개](****[https://joshua1988.github.io/vue-camp/vuex/concept.html](https://joshua1988.github.io/vue-camp/vuex/concept.html))
- [**컴포넌트 데이터 전달 방법]**([https://developerjournal.tistory.com/4](https://developerjournal.tistory.com/4))
- [****Vuex란?]****([https://junho94.tistory.com/20?category=846133](https://junho94.tistory.com/20?category=846133))

---

## 더 알아보기

- [서버사이드의 레이스컨디션](https://velog.io/@nuxt/Nuxt.js-VuexStore) 을 막기 위해 store의 state는 함수형으로 작성한다?

[https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbwQByt%2FbtqAlQpvCcZ%2F4EOdCgiZ6KtdVjtTemhjbk%2Fimg.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbwQByt%2FbtqAlQpvCcZ%2F4EOdCgiZ6KtdVjtTemhjbk%2Fimg.png)
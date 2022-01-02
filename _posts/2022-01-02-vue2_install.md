---
title: "nodejs, vue-cli 설치 및 개발환경 셋팅 "
excerpt: "유튜브 코딩애플 - 펻"
categories:
  - Client
tags:
  - Vue3
  - Nodejs
  - Installation
toc: true
toc_sticky: true
toc_label: 목차
toc_icon: "cog"
# classes: wide
header:
  teaser: /assets/images/2022-01-02/Untitled.png
---

**[참고]** [유튜브 코딩 애플](https://youtu.be/NONWar0jGLM)

## 1.개발환경 설치

### 1) 사이트에서 `nodejs` 설치 (16.13.1 LTS로 설치함)

- 가장 최신의 LTS 버전을 받으면 됩니다
- 🧐 nodejs 왜 설치해야 함?? → npm 쓰려고!
  - `npm`: 웹개발 관련 라이브러리들을 쉽게 쓸 수 있도록 도와주는 패키지 매니저
  - `npm`을 쓰면 `vue-cli`를 쉽게 설치할 수 있다.
  - `**vue-cli**` : vue 프로젝트를 빠르게 생성해주는 라이브러리

![Untitled](/assets/images/2022-01-02/Untitled.png)

### 2) 터미널에서 `**vue-cli**` 설치

```bash
npm install -g @**vue/cli**
```

![Untitled](/assets/images/2022-01-02/Untitled%201.png)

- npm 설치에서 버전 관련 에러 발생 → `npm install -g npm@8.3.0 to update!`
- 바로 8.3.0 버전으로 명령어를 쳤더니 permission 에러 발생 → sudo 붙여줌

![Untitled](/assets/images/2022-01-02/Untitled%202.png)

![버전 확인](/assets/images/2022-01-02/Untitled%203.png)

버전 확인

### 3) vs code 부가 플러그인 설치

- vetur
- html css support
- vue 3 snippets

## 2. 프로젝트 생성

### 1) 작업용 폴더 생성

![Untitled](/assets/images/2022-01-02/Untitled%204.png)

### 2) vs code에서 [File] - [Open Folder...] 으로 해당 작업 폴더 열기

![Untitled](/assets/images/2022-01-02/Untitled%205.png)

### 3) 터미널에 입력

```bash
vue create 프로젝트명
```

선택하라고 뭐가 나오면 Vue3을 선택한다

![Untitled](/assets/images/2022-01-02/Untitled%206.png)

그러면 작업폴더 하위에 터미널로 입력한 프로젝트가 생성된다.

![Untitled](/assets/images/2022-01-02/Untitled%207.png)

### 4) 이렇게 생성된 프로젝트를 에디터로 연다.

![굵은 글씨로 만든 프로젝트 명이 되어 있어야 성공-✨](/assets/images/2022-01-02/Untitled%208.png)

굵은 글씨로 만든 프로젝트 명이 되어 있어야 성공-✨

### 5) App.vue에서 코드를 짜면 됨!

여기가 메인 페이지이다.

![Untitled](/assets/images/2022-01-02/Untitled%209.png)

### 6) 미리보기로 보고싶으면 npm run serve를 쳐서 확인

![코드를 수정하면 바로바로 반영되어 볼 수 있다.](/assets/images/2022-01-02/Untitled%2010.png)

코드를 수정하면 바로바로 반영되어 볼 수 있다.

> 📌 <b> App.vue를 브라우저가 어떻게 읽을 수 있지??</b>
>
> - App.vue에 있던 파일을 index.html에 박아넣어서 컴파일되어 볼 수 있는 것이다.
> - 이 박아넣는 작업은 main.js에서 이루어진다.

## +) 폴더/파일 설명

- node_modules : 프로젝트에 쓰는 모든 라이브러리들
- src : 소스코드 다 담는 곳. 실제로 코드 짜는 공간
- public : html파일, 기타 파일 보관
- 🌟 `package.json` : 설치한 라이브러리들의 버전, 프로젝트 설정 기록

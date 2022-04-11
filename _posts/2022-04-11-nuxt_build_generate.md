---
title: "Nuxt의 generate 배포 옵션"
excerpt: "npm run dev만 알면 되는거 아닌가여? generate는 어따쓰죵??"
categories:
  - Client
tags:
  - Nuxt
  - deploy
  - build
toc: true
toc_sticky: true
toc_label: 목차
toc_icon: "list"
# header:
  # teaser: /assets/images/2022-04-03/after.png
---
## TL;DR 
> Nuxt의 generate 배포 옵션은 `Vue.js 애플리케이션을 정적으로 생성`하는 옵션으로, 정적 호스팅에 사용됩니다. (저의 경우 Spring Boot와 Nuxt를 연동할 때 사용했습니다.) <br>
프론트엔드를 빌드했을때 결과물의 경로를 백엔드의 static 폴더로 들어가게 하여 개발 및 운영서버에 함께 배포할 수 있도록 설정합니다. 

## build

- 웹팩을 통해 애플리케이션을 빌드.
- nuxt.config.json의 `target:’server’`가 설정되어 있을때 `npm run build`를 실행하면 .nuxt/dist에 파일들이 생성됩니다.
- Node.js 서버에 배포할때 쓰는 용도

## generate

- nuxt.config.json에서 `target:’static’`이 설정되어 있을 때 `npm run generate`를 실행함으로써 파일들이 생성됩니다
- Netllify나 Vercel, Firebase Hosting 등의 호스팅 서비스에 배포할 때 쓰는 용도
- generate의 빌드 결과물은 default로 dist디렉토리로 되어 있지만 nuxt.config내에서 변경 가능합니다.
    
    제가 속한 프로젝트의 경우(Spring boot + Nuxt) 아래와 같이 static 폴더로 빌드 결과물이 떨어지게 설정되어 있습니다.
    
   <figure>
    <img src='{{ "/assets/images/2022-04-11/Untitled.png" | relative_url }}' width="450" />
  </figure>
    
    ```
    generate : {
        dir : "../../src/main/resources/static",
      },
    ```
    
- `nuxt generate` : 정적 생성 (사전 렌더링)
    - Vue.js 애플리케이션을 정적으로 생성하는 옵션.
    - 애플리케이션을 빌드할 때 **모든 라우트를 HTML로 생성**하는 명령어.
- 예시) 예를 들어 다음과 같은 파일 구조가 있습니다.
    
    ```
    -| pages/
    ----| about.vue
    ----| index.vue
    ```
    
    이는 아래와 같이 생성됩니다.
    
    ```
    -| dist/
    ----| about/
    ------| index.html
    ----| index.html
    ```
    
    이렇게 하면 생성된 웹 어플리케이션을 모든 정적 호스팅에서 호스팅할 수 있습니다. 
    
- Spring boot 백엔드 프로젝트에 프론트엔드 작업 결과물을 포함시켜 하나의 컴파일된 파일을 배포 및 운영하기 위해 이러한 작업을 합니다.
    
    ([https://deockstory.tistory.com/26](https://deockstory.tistory.com/26))
    

### +) [명령어 리스트](https://develop365.gitlab.io/nuxtjs-0.10.7-doc/ko/guide/commands/)

아래의 명령문들을 package.json에 작성해야 합니다. 그 후 `npm run <command>` 명령어를 통해 서버를 시작할 수 있습니다. 

- `nuxt` : 개발서버를 핫 리로딩 상태로 localhost:3000에 시작합니다.
- `nuxt build` : Webpack을 통해 어플리케이션을 빌드하며, CSS와 JS를 최소화하는 작업을 진행합니다. (프로덕션용으로)
- `nuxt start` : 프로덕션 모드로 서버를 시작합니다. (nuxt build 실행 후)
- `nuxt generate` : 어플리케이션을 빌드하고 모든 라우트를 HTML 파일로 생성합니다.

1) 개발환경 : nuxt 아니면 npm run dev

2) 프로덕션 배포 : SSR모드 혹은 정적 파일 생성 모드 중 한 가지를 선택할 수 있습니다. 

- SSR 환경 : nuxt build → nuxt start
- 정적 파일 생성 환경 : npm run generate

---

### 참고

- **Nuxt에서 Firebase로 Hosting하기(build와 generate 차이) :** [https://heewon26.tistory.com/372](https://heewon26.tistory.com/372)
- ****[Nuxt.js] 개념부터 설치까지 빠르게 배우기 :**** [https://kdydesign.github.io/2019/04/10/nuxtjs-tutorial/](https://kdydesign.github.io/2019/04/10/nuxtjs-tutorial/)
- ****[Nuxt.js] Nuxt 학습기 - (2) LifeCycle & 렌더링 모드:**** [https://abangpa1ace.tistory.com/205](https://abangpa1ace.tistory.com/205)
- [https://github.com/AhaOfficial/nuxt-template/blob/master/docs/실행_빌드_배포_방법.md](https://github.com/AhaOfficial/nuxt-template/blob/master/docs/%EC%8B%A4%ED%96%89_%EB%B9%8C%EB%93%9C_%EB%B0%B0%ED%8F%AC_%EB%B0%A9%EB%B2%95.md)
- [https://jamong-icetea.tistory.com/207](https://jamong-icetea.tistory.com/207)
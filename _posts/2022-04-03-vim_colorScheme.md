---
title: "vim color scheme 변경하기"
excerpt: "원래 에디터는 예뻐야 쓸 맛이 나는거쟈나여? 쓸 맛이 나야 공부도 하고 그런 거자나여?"
categories:
  - Vim
tags:
  - vim
toc: true
toc_sticky: true
toc_label: 목차
toc_icon: "list"
header:
  teaser: /assets/images/2022-04-03/after.png
---


## TL;DR 
> vim 설정 파일인 ~/.vimrc 파일에 `:colorscheme [원하는 scheme]` 을 추가한다


## 참고 링크
[VIM Color Scheme 변경하기](https://rottk.tistory.com/entry/VIM-Color-Scheme-%EB%B3%80%EA%B2%BD%ED%95%98%EA%B8%B0)

[Color Scheme(색깔) 바꾸기](https://blog.leocat.kr/notes/2017/07/26/vi-vim-change-colour-scheme)

## vim color scheme 확인하기

- 컬러 테마들은 보통 /usr/share/vim/vim[버전]/colors 에 위치한다.
   
  <figure>
    <img src='{{ "/assets/images/2022-04-03/vim_colors_path.png" | relative_url }}' width="850" />
    <figcaption>colors 경로</figcaption>
  </figure>
    
- 원하는 테마를 받아서 쓸 수도 있다. -O 옵션 뒤에 vim이 설치된 경로를 넣는다.
    
    ```bash
    sudo wget https://raw.githubusercontent.com/nanotech/jellybeans.vim/master/colors/jellybeans.vim -O /usr/share/vim/vim74/colors/jellybeans.vim
    ```
- 테마 추천 10개     
  - [http://www.vimninjas.com/2012/08/26/10-vim-color-schemes-you-need-to-own/](http://www.vimninjas.com/2012/08/26/10-vim-color-schemes-you-need-to-own/)

## color scheme 지정

- vim 설정파일인 .vimrc 파일을 이용해서 vim 시작시 사용할 기본 color scheme을 지정할 수 있다.
    - /etc/vimrc 파일을 수정하면 모든 사용자의 설정이 변경됨
    - ~/.vimrc 파일을 수정하면 현재 로그인한 사용자의 설정만 변경됨
    
    ```bash
    # 없으면 생성해도 됨
    vim ~/.vimrc
    ```
    
- 예를 들어, 다운받은 jellybeans.vim을 적용하고 싶다면 아래 내용을 파일에 추가한다.
    
    ```bash
    colo jellybeans
    syntax on
    ```
    
    또는
    
    ```bash
    :colorscheme jellybeans
    ```
    

### 적용한 모습

- 적용 전
    
  <figure>
    <img src='{{ "/assets/images/2022-04-03/before.png" | relative_url }}' width="850" />
  </figure>
    
- jellybeans 적용 후
    
  <figure>
    <img src='{{ "/assets/images/2022-04-03/after.png" | relative_url }}' width="850" />
  </figure>
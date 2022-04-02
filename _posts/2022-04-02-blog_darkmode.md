---
title: "minimal-mistakes 다크모드 토글버튼 적용하기"
excerpt: "jekyll 블로그에 다크모드를 적용해보자!"
categories:
  - Blog
tags:
  - dark mode
  - jekyll
toc: true
toc_sticky: true
toc_label: 목차
toc_icon: "list"
# classes: wide
# header:
  # teaser: /assets/images/2022-01-02/Untitled.png
---


## TL;DR 
> theme2 를 만들어서 적용한다

## 참고 링크

**[Vladsiv](https://www.vladsiv.com/) 님의 [코드](https://github.com/VladimirSiv/VladimirSiv.github.io/tree/3985fe26e6a9572098945b7b5409bb6e540529a4)를 참고하여 적용했습니다.**

[Allow user to toggle between themes [light/dark] · Discussion #2033 · mmistakes/minimal-mistakes](https://github.com/mmistakes/minimal-mistakes/discussions/2033#discussioncomment-2217062)


## _config.yml

저는 기본을 다크모드로 설정하고 싶어서 skin을 dark로 하고 skin2를 default로 했습니다.

```yaml
minimal_mistakes_skin: "dark" # "air", "aqua", "contrast", "dark", "dirt", "neon", "mint", "plum", "sunrise"
minimal_mistakes_skin2   : "default"
```

## _includes/head.html

```html
<!-- ... -->

<!-- For all browsers -->
<!-- <link rel="stylesheet" href="{{ '/assets/css/main.css' | relative_url }}"> -->
<link rel="stylesheet" href="{{ '/assets/css/main.css' | relative_url }}" id="theme_source">
{% if site.minimal_mistakes_skin2 %}
<link rel="stylesheet alternate" href="{{ '/assets/css/theme2.css' | relative_url }}" id="theme_source_2">

<script>
  let theme = sessionStorage.getItem('theme');
  if (theme === "dark") {
    sessionStorage.setItem('theme', 'dark');
    node1 = document.getElementById('theme_source');
    node2 = document.getElementById('theme_source_2');
    node1.setAttribute('rel', 'stylesheet alternate');
    node2.setAttribute('rel', 'stylesheet');
  }
  else {
    sessionStorage.setItem('theme', 'light');
  }
</script>
{% endif %}

<link rel="preload" href="https://cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@5/css/all.min.css" as="style"
  onload="this.onload=null;this.rel='stylesheet'">
<noscript>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@5/css/all.min.css">
</noscript>
<!-- ... -->

```

## _includes/masthead.html 에 아이콘 추가

```html
(...중략)

<ul class="visible-links">
  {%- for link in site.data.navigation.main -%}
    <li class="masthead__menu-item">
      <a href="{{ link.url | relative_url }}"{% if link.description %} title="{{ link.description }}"{% endif %}>{{ link.title }}</a>
    </li>
  {%- endfor -%}
</ul>

 <!-- 다크 모드 토글 버튼 -->
{% if site.minimal_mistakes_skin2 %}
  <i class="fas fa-fw fa-adjust" aria-hidden="true" onclick="node1=document.getElementById('theme_source');node2=document.getElementById('theme_source_2');if(node1.getAttribute('rel')=='stylesheet'){node1.setAttribute('rel', 'stylesheet alternate'); node2.setAttribute('rel', 'stylesheet');sessionStorage.setItem('theme', 'dark');}else{node2.setAttribute('rel', 'stylesheet alternate'); node1.setAttribute('rel', 'stylesheet');sessionStorage.setItem('theme', 'light');} return false;"></i>
{% endif %}

{% if site.search == true %}
  <button class="search__toggle" type="button">
    <span class="visually-hidden">{{ site.data.ui-text[site.locale].search_label | default: "Toggle search" }}</span>
    <svg class="icon" width="16" height="16" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 15.99 16">
      <path d="M15.5,13.12L13.19,10.8a1.69,1.69,0,0,0-1.28-.55l-0.06-.06A6.5,6.5,0,0,0,5.77,0,6.5,6.5,0,0,0,2.46,11.59a6.47,6.47,0,0,0,7.74.26l0.05,0.05a1.65,1.65,0,0,0,.5,1.24l2.38,2.38A1.68,1.68,0,0,0,15.5,13.12ZM6.4,2A4.41,4.41,0,1,1,2,6.4,4.43,4.43,0,0,1,6.4,2Z" transform="translate(-.01)">
      </path>
    </svg>
  </button>
{% endif %}

(...중략)
```

## assets/css/theme2.scss 추가

```css
---
# Only the main Sass file needs front matter (the dashes are enough)
---

@charset "utf-8";

@import "minimal-mistakes/skins/{{ site.minimal_mistakes_skin2 | default: 'default' }}"; // skin
@import "minimal-mistakes"; // main partials
```

---
title: "IE에서 ES6문법이 안될때 폴리필 사용하기 (feat. JSP)"
excerpt: "으으..IE..너만 없으면..!!!"
categories:
  - Client
tags:
  - IE
  - polyfill
  - Javascript
toc: true
toc_sticky: true
toc_label: 목차
toc_icon: "list"
# header:
  # teaser: /assets/images/2022-04-03/after.png
---


## TL;DR 
> 폴리필을 쉽게 사용하려면 [폴리필io](https://polyfill.io/v3/url-builder/)에서 필요한 기능을 구성해서 사용하고자 하는 곳보다 더 먼저 cdn을 넣어주면 된다.

---

## 왜 슬픈 예감은 틀리지 않는지..

개발이 끝나고 얼추 잠잠한가 싶었는데, 크롬에서는 정상 작동하는 기능이 IE에서 안된다는 이슈를 받았다.

확인해보니 IE에서 includes를 지원하지 않는다는 문구가 새빨갛게 불타고 있었다....ㅎ

그냥 넘어갔으면,, 싶었지만 사용자의 70% 정도는 IE 사용자라고 해서,, 꼭 해결하고 넘어가야 했다. 

<figure>
    <img src='{{ "/assets/images/2022-04-07/Untitled.png" | relative_url }}' width="850" />
    <figcaption>불타오르는 IE의 경고</figcaption>
</figure>

<figure>
    <img src='{{ "/assets/images/2022-04-07/Untitled 1.png" | relative_url }}' width="850" />
    <figcaption>includes를 지원하지 않는구나.. 그렇구나</figcaption>
</figure>

대표님께 여쭤보니 이런 경우 웹팩을 쓰면 바벨이 되니까 상관없지만, 이 녀석같은 레거시,,ㅎ 는 폴리필을 사용하면 된다고 하셨다. 

## 폴리필이요..?
먼저, 크롬이나 엣지, 파이어폭스, IE 등 이러한 브라우저는 그마다 지원하는 기능이 다르다. 구형 브라우저일수록 최신 기능을 지원하지 않는 것은 인지상정..

[폴리필은 IE같은 구형 브라우저에서 동작하지 않는 최신 기능을 동작할 수 있도록 도와주는 기술이다.](https://jforj.tistory.com/210)

+) [하지만 폴리필 플러그인 로드 때문에 시간과 트래픽이 늘어나고, 브라우저별 기능을 추가하는 것이기 때문에 코드가 매우 길어지고 성능이 많이 저하된다는 단점이 있다.](https://jcon.tistory.com/123)


## 적용하기
### 1. 지원하지 않는 기능 확인하기
[Can I use](https://caniuse.com/) 사이트에서 IE가 지원하지 않는 것을 확인한다.
<figure>
    <img src='{{ "/assets/images/2022-04-07/canIuse.png" | relative_url }}' width="850" />
</figure>

### 2. 폴리필 찾아서 적용하기
폴리필 파일을 다운받거나, 코드를 복붙하거나, [Polyfill.io](https://polyfill.io/v3/url-builder/)에서 cdn을 사용하거나
- 코드 복붙
    - 구글에 기능명과 polyfill을 함께 검색해서 모질라 재단에 나온 폴리필 코드를 사용하는 코드 바로 위에 붙여 넣는다.
    <figure>
        <img src='{{ "/assets/images/2022-04-07/mozilla.png" | relative_url }}' width="850" />
    </figure>


- cdn 사용하기
    - URL을 구성해서 사용하려는 곳보다 먼저 로드되도록 넣어준다.
    <figure>
        <img src='{{ "/assets/images/2022-04-07/polyfillCdn.png" | relative_url }}' width="850" />
        <figcaption>Polyfill.io에서 원하는 기능을 체크하여 cdn을 구성한다</figcaption>
    </figure>



## 그리고 나온 또다른 문제...1
includes 외에도 내가 캐치하지 못한 다른 기능들이 있을 수 있으니까 상세한 기능을 설정하지 않고 min파일 그대로 cdn을 넣었더니,,

<figure>
    <img src='{{ "/assets/images/2022-04-07/Untitled 2.png" | relative_url }}' width="850" />
    <figcaption>polyfill 소스 내부에 있는 속성을 못읽는다고...?</figcaption>
</figure>

이런 에러가 발생했다.. ㅎ 
폴리필은 성능에도 저하가 발생한다고 하니,, 필요한 기능만 넣어서 사용하는 것이,, 좋겠습니다,, ㅎ


## 그리고 나온 또다른 문제...2
저 includes()가 들어있는 write.js가 있고, 나는 이 write.js를 import하는 write.jsp쪽에 폴리필 cdn을 넣었는데 계속 적용이 되지 않았다...

이것 저것을 시도해 본 결과, 나의 경우에는 메일쓰기 팝업인 write.jsp에 넣는 대신 홈페이지 처음 들어올때 부르는 resources.jsp에서 먼저 부르도록 했더니 적용이 되었다. <br>
확실하게 사용 시점보다 더 빨리 폴리필이 로드되어야 하는게 맞나보다.

<figure>
    <img src='{{ "/assets/images/2022-04-07/Untitled 3.png" | relative_url }}' width="850" />
    <figcaption>resources.jsp</figcaption>
</figure>

<figure>
    <img src='{{ "/assets/images/2022-04-07/Untitled 4.png" | relative_url }}' width="850" />
    <figcaption>에러가 사라진 깨끗한 모습</figcaption>
</figure>

콘솔에 아무 에러 없이 해결되었다고 한다.. ㅎ
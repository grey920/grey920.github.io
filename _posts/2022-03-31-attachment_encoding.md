---
title: "Commons Email로 메일 발송시 첨부파일명 한글 깨짐 현상"
excerpt: "뭐야 아파치.. 한글 무ssi해..?"
categories:
  - Server
tags:
  - SMTP
  - java
  - encoding
  - File
toc: true
toc_sticky: true
toc_label: 목차
toc_icon: "list"
# classes: wide
# header:
  # teaser: /assets/images/2022-01-02/Untitled.png
---

## TL;DR 
> 서버 구동시 `-Dmail.mime.encodeparameters=false` 를 추가한다


## 현상
apache commons email API를 사용해서 SMTP로 메일 발송을 테스트하던 중 첨부파일명이 한글이면 인코딩이 깨지는 현상이 발견되었습니다... 
<br>
아무리 setCharset("UTF-8")을 해줘도 이상하게 첨부파일명만! 한글이 들어가면 깨졌죠..

<figure>
<img src='{{ "/assets/images/2022-03-31/1.png" | relative_url }}' width="850" />
<figcaption>회사 메일로 보낸 경우</figcaption>
</figure>

<figure>
<img src='{{ "/assets/images/2022-03-31/2.png" | relative_url }}' width="850" />
<figcaption>구글 메일로 보낸 경우</figcaption>
</figure>

## 해결
`-Dmail.mime.encodeparameters=false` 옵션을 System property로 추가합니다. <br>
Java Mail이 업데이트 되면서 생긴 이슈인가 봅니다.<br>
Commons Email이 내부적으로 Java Mail을 사용하고 있기 때문에 영향을 받은 것 같고, <br>
mail.mime.encodeparameters을 false로 시스템 프로퍼티를 셋팅하면 메세지를 생성할때 RFC 2231 지원을 막는다고 합니다.<br> (Set the System property mail.mime.encodeparameters to false. This disables the RFC 2231 support when creating messages.)

<figure>
<img src='{{ "/assets/images/2022-03-31/4.png" | relative_url }}' width="850" />
<figcaption>테스트코드 구동</figcaption>
</figure>

<figure>
<img src='{{ "/assets/images/2022-03-31/5.png" | relative_url }}' width="850" />
<figcaption>개발서버에서 구동 (catalina.sh)</figcaption>
</figure>

<figure>
<img src='{{ "/assets/images/2022-03-31/3.png" | relative_url }}' width="850" />
<figcaption>처리된 모습</figcaption>
</figure>


---
### 참고 링크
[java mail 발송시 첨부파일 한글 깨짐 현상](https://zzangjava.tistory.com/977?category=507221)<br>
[Issue with JavaMail attachment names](https://stackoverflow.com/questions/34128695/issue-with-javamail-attachment-names)
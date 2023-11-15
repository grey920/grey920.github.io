---
title: "HTTPS, DNS, UDP 그리고 신뢰적 데이터 전송"
excerpt: ""
categories:
  - CS
tags:
  - JS 스터디
  - 네트워크
toc: true
toc_sticky: true
toc_label: "HTTPS, DNS, UDP 그리고 신뢰적 데이터 전송"
toc_icon: "edit"
# classes: wide
header:
  overlay_image: 'https://images.velog.io/images/jhlee508/post/516e42f6-5c80-4919-ab07-c8fa54ab574d/%EC%BB%B4%ED%93%A8%ED%84%B0%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC.jpg'
  teaser: /assets/images/2022-01-02/Untitled.png #/assets/images/2022-01-02/Untitled.png
---
## HTTPS
### HTTPS? HTTP랑 다른가?
<figure>
  <img src="https://www.cloudflare.com/img/learning/security/glossary/what-is-https/not-secure.png">
  <figcaption>https://www.cloudflare.com</figcaption>
  <figcaption>브라우저에서는 HTTPS가 아닌 모든 웹사이트는 안전하지 않은 것으로 표시된다.</figcaption>
</figure>


HTTPS는 웹 서버와 웹 브라우저 간에 데이터를 안전하게 보내기 위한 방법으로, 웹 상에서 데이터 전송시 사용되는 기본 프로토콜인 **HTTP**에서 `보안`이 강화된 프로토콜이다. 데이터 전송의 보안을 강화하는 방법으로 **암호화**를 사용한다.

### 꼭 보안을 강화해야 할까?
먼저 일반 HTTP를 이용해 정보를 전송하면, 데이터는 쉽게 스니핑(탈취나 감시) 할 수 있는 데이터 **패킷**으로 나뉜다. <br>
HTTP를 통한 모든 통신은 **일반 텍스트**로 이루어지므로 도구만 있으면 누구나 쉽게 데이터에 접근할 수 있다.<br>
우리가 웹 상에서 전송하는 데이터에는 은행 계좌나 의료 정보, 로그인 정보와 같이 중요한 데이터들도 포함되기 때문에 일반 텍스트로 전송된다면 스니핑을 통해 악의적으로 정보가 사용될 가능성이 있다.<br>
하지만 HTTPS를 사용하면 트래픽이 **암호화 프로토콜(TLS)** 을 사용하여 `암호화`되기 때문에 패킷을 스니핑하거나 가로챈다고 해도 **무의미한 문자**로만 인식된다.<br>

### SSL/TLS란?
HTTPS는 특정 공급자가 주장하는 실체가 맞는지 확인하는 **TLS/SSL 인증서**의 전송을 기반으로 이루어진다.<br>
`TLS/SSL`은 인터넷 트래픽을 암호화하고 서버 신원을 확인하기 위한 **프로토콜**이다. TLS는 넷스케이스사가 개발한 SSL 암호화 프로토콜에서 발전한 것으로, TLS 버전 1.0은 SSL 버전 3.1로서 개발을 시작했지만 넷스케이프사와 더 이상 연관이 없음을 명시하기 위해 발표 전 이름이 변경되었다.

### TLS가 하는 일이 뭐야?
1. 암호화 : 전송되는 데이터를 숨긴다
2. 인증 : 정보를 교환하는 당사자가 요청된 당사자임을 보장한다.
3. 무결성 : 데이터가 위조되거나 변조되지 않았는지 확인한다.

### HTTPS의 암호화 과정
<img src="https://cf-assets.www.cloudflare.com/slt3lc6tev37/3wZIhjRIjfVSmCbVqkBKzb/4a7aa34324108c725dc25fc9e7c4ea4a/tls-ssl-handshake.png">

클라이언트가 웹 페이지에 연결하면 웹 페이지에서 보안 세션을 시작하는 데 필요한 공개키가 포함된 SSL 인증서를 전송한다. 그런 다음 클라이언트와 서버가 보안 연결을 설정하는 데 사용되는 `TLS handshake 프로세스`를 거친다. 

#### TLS handshake
TLS handshake는 TLS 암호화를 사용하는 통신 세션을 실행하는 프로세스로 TCP 연결이 TCP handshake를 통해 열린 후에 발생한다.

TLS handshake 과정 중에 클라이언트와 서버는 함께 다음의 작업을 수행한다.
- 사용할 TLS 버전 지정
- 사용할 암호 알고리즘 세트 결정
- 서버의 공개 키와 SSL 인증서 기관의 디지털 서명을 통해 서버의 ID 인증
- handshake가 완료된 후에 대칭 암호화를 사용하기 위하여 세션 키 생성

#### TLS handshake 단계
1. 


### 대칭키와 비대칭키
<figure>
  <img src="https://velog.velcdn.com/images%2Fminj9_6%2Fpost%2Fd5082238-3853-4523-bae9-44f83a1dc0e9%2Fimage.png">
  <figcaption>https://velog.io/@minj9_6/%EB%8C%80%EC%B9%AD%ED%82%A4%EC%99%80-%EB%B9%84%EB%8C%80%EC%B9%AD%ED%82%A4%EB%8A%94-%EB%AC%B4%EC%8A%A8-%EC%B0%A8%EC%9D%B4%EA%B0%80-%EC%9E%88%EC%9D%84%EA%B9%8C</figcaption>
</figure>

대칭키는 암호화에 사용하는 키와 복호하에 사용하는 키가 대칭을 이룬다. 즉, 동일한 키를 사용한다.<br>
반면 비대칭키는 암호화와 복호화에 사용하는 암호키를 분리한다. <br>

`대칭키 암호화 방식`은 키만 가지고 있으면 누구나 암호문을 복호화할 수 있기 때문에 간편하고 **속도가 빠르다.** 하지만 암호화한 사람이 복호화 할 사람에게 키를 어떻게 안전하게 건네줄 수 있는지에 대한 문제가 생긴다. ( **키 배송 문제** )<br>
키를 교환하는 중에 **키가 탈취**될 수 있고, 사용자가 증가할수록 전부 각자 키를 교환해야 하므로 **관리해야 할 키가 무수히 많아질 수 있다**. <br>

**키 배송 문제**를 해결하기 위한 방법으로 나온 것 중 하나가 `비대칭키(공개키) 암호화 방식`이다. <br>
`개인 키`는 타인에게 절대 노출되면 안되는 비밀 키이다. 키 소유자는 전달받은 암호문을 개인 키로 복호화할 수 있다. `공개 키`는 개인키를 토대로 만든 키이며 이름 그대로 대중에게 공개된 키이기 때문에 모두가 접근할 수 있어 **키를 교환할 필요가 없다**. 이 2 개의 키가 쌍을 이룬 형태가 비대칭키이다.

#### 비대칭 키의 개인 키와 공개 키
<figure>
  <img src="https://github.com/grey920/obsidian_tech-note/assets/58028215/a96de342-b874-4858-8d20-5da300cc67cf">
  <figcaption>출처:http://cryptocat.tistory.com/3</figcaption>
</figure>



A가 B에게 암호문을 보낸다고 한다면 다음과 같다. 
1. A가 전송하고 싶은 평문 =>  B의 `공개키`로 **암호화** => 암호문 생성
2. B가 전달받은 암호문 =>  B가 가지고 있던 `개인키`로 **복호화** => 평문 
이렇게 만들어진 암호문은 B에게만 유효하기 때문에 `공개키`는 외부 모두에게 노출되어도 상관이 없지만, ✨`개인키`는 **보안**이 유지되어야 한다.

## DNS
### DNS가 뭐야?
`DNS`란 (Domain Name System) 의 약자로 도메인 이름의 **계층적인 체계**를 말한다.<br>
네트워크 상에서 컴퓨터들은 IP주소를 이용하여 서로를 구별하고 통신한다. 하지만 숫자의 연속인 IP주소를 사람들이 일일이 외울 수 없기 때문에 쉽게 기억할 수 있도록 도메인 주소 체계가 만들어졌다.
<figure>
  <img src="https://한국인터넷정보센터.한국/images/domain/imgDomainSys02.gif">
  <figcaption>출처: https://xn--3e0bx5euxnjje69i70af08bea817g.xn--3e0b707e/jsp/resources/dns/dnsInfo.jsp</figcaption>
</figure>




### DNS는 어떻게 작동할까?
도메인은 계층 구조로 되어 있으며 상위 도메인부터 하위 단계로 순서대로 주소를 찾아간다.<br>
예를 들어, 구글 도메인을 브라우저에 입력한다면 .com → .google → www 순으로 주소 검색이 진행된다.

#### DNS 서비스 유형
모든 DNS 서버는 네 가지 카테고리로 분류된다.
- 재귀 확인자
- 루트 네임서버
- TLD 네임서버
- 권한 있는 네임서버

#### DNS 작동 방식
다음은 DNS를 통해 IP 주소를 찾아오는 작동 방식이다.
<figure>
  <img src="https://d1.awsstatic.com/Route53/how-route-53-routes-traffic.8d313c7da075c3c7303aaef32e89b5d0b7885e7c.png">
  <figcaption>출처: https://aws.amazon.com/ko/route53/what-is-dns/</figcaption>
</figure>



1. 사용자가 웹 브라우저에 도메인 이름 또는 URL을 입력한다. -> **사용자 로컬 PC의 메모리**를 확인한다 <br>
	1) 로컬 PC 메모리의 **\*DNS Cache**에 해당 IP가 있는지 확인한다.<br>
	2) 로컬PC 메모리에도 주소가 없다면, **hosts 파일**을 검색한다.<br>
	3) **공유기**가 DNS 포워딩 기능을 해서 DNS처럼 응답을 대리하기도 한다.
2. 1.에서 주소를 찾을 수 없다면 **\*ISP가 제공하는 DNS 서버(해석기)**로 쿼리한다. ( `재귀적 쿼리` )
	- 클라이언트와 DNS 사이의 중개자는 재귀 확인자 또는 DNS 리커서라고 한다. (위의 그림에서 DNS resolver)
	- 재귀 확인자(재귀 리졸버) 라는 명칭은 주어진 이름에 대한 각 쿼리를 수행하고 **최종 결과를 반환**한다는 데에서 비롯되었다.
1. ISP의 DNS 서버는 본인에 캐싱된 IP주소가 없다면 **루트 DNS 서버**에 해당 도메인에 대한 IP 주소를 요청한다. 루트 DNS 서버는 .com과 같은 최상위 도메인 (Top-Level Domain, TLD) 서버의 IP를 응답한다.
2. 로컬 DNS 서버는 **TLD 서버**에 다음 계층 주소를 포함하는 하위 DNS 서버의 IP 주소를 요청한다.(`반복적 쿼리`)
3. 같은 방식으로 계층 하나씩 이동하며 최종 도메인의 IP 주소를 받을 때까지 쿼리를 반복한다.
4. 최종 DNS 서버에서 해당 도메인의 IP 주소를 반환하고 로컬 DNS 서버는 이를 브라우저 PC와 자신의 캐시에 저장하고 사용자에게 IP 주소를 전달한다.

> \* DNS 캐시 <br>
> PC 내 작은 임시 전화번호부와 같은 개념이다. 여기에 최근 방문한 사이트의 도메인 정보와 IP 주소를 기록해둔다. 대부분의 경우 최근에 방문한 사이트를 다시 방문하는 경우가 많기 때문에 캐싱된 주소를 바로 사용하는 것은 굉장히 효율적인 방법이다. <br>
> 하지만 **DNS 캐시가 오염**되는 경우 사용자가 특정 도메인을 입력했을 때 의도치 않은 사이트로 이동하게 된다. 이는 악의적인 목적을 가진 해커로부터 좋은 공격 대상이 된다. => 따라서 주기적으로 한 번씩  DNS 서버를 정리할 필요가 있다. 이러한 DNS 서버 정리를 `DNS Flushing` 이라 한다.

> * ISP가 제공하는 DNS 서버 <br>
> ISP는 인터넷 서비스 제공자(Internet Service Provider)로 우리나라의 경우 가장 대표적인 유선 인터넷 ISP는 kt, lg유플러스, sk브로드밴드 가 있다.
> 그리고 ISP 사업자별로 대표 DNS가 등록되어 있다. <br>
> **KT** 기본 DNS 서버 : 168.126.63.1 <br>
> **SK** 기본 DNS 서버 : 210.220.163.82 <br>
> **LG** 기본 DNS 서버 : 164.124.101.2 <br>
> **Google** 기본 DNS 서버 : 8.8.8.8 <br>

### DNS 쿼리(질의) 종류
- 클라이언트에서 로컬 DNS 서버로 이름 분석 결과만 알려달라고 보내는 요청을 재귀적(recursive) 쿼리라고 한다.
- 그리고 요구하는 IP 주소가 없을 때 로컬 DNS에서 root DNS 서버 및 하위 DNS 서버에 같은 쿼리를 보내는 것을 반복적 (iterative) 쿼리라고 한다. 
- 재귀적 쿼리는 도메인 이름에 대한 각 쿼리를 수행하고 최종 결과를 반환하지만, 반복적 쿼리는 답을 알 수 있는 다음 DNS 서버에 대한 참조만 반환한다는 차이가 있다. 

### DNS 레코드
DNS 레코드란 DNS에 받은 요청을 어떻게 처리할 것인지에 대한 정보라고 볼 수 있다.
각 개별 레코드에는 유형(이름 및 번호), TTL(Time to live, 수명), 유형별 데이터를 포함한다.

#### 일반적인 DNS 레코드 종류
- A 레코드
- AAAA 레코드
- CNAME 레코드
- MX 레코드
- TXT 레코드
- NS 레코드

### DNS 서버에 IP 주소를 요청할 때 왜  TCP가 아닌`UDP`를 쓸까?
DNS가 신뢰성보다는 **속도**가 더 중요한 서비스라는 특징 때문!

TCP의 경우 3way-handshaking 과정이 있지만 UDP는 이러한 연결 설정 및 해제의 오버헤드가 발생하지 않기 때문에 빠른 응답을 요하는 DNS에는 `UDP`가 적합하다.

## UDP
### UDP란?
UDP(User Datagram Protocol)는 연결을 설정하지 않고 데이터를 전송하는 간단한 통신 프로토콜이다. 
**신속**한 데이터 전송을 지원하며, 특히 작은 규모의 패킷 통신에 적합하다. 
그러나 **신뢰성은 보장하지 않고**, 패킷 손실이나 순서 변경이 발생할 수 있다.
즉, TCP와 UDP의 차이 중 하나는 바로 **신뢰적인 서비스를 제공**해주냐 의 차이이다. 

### UDP의 장단점
**UDP의 장점:**
1. **낮은 지연 시간:** 연결 설정과 해제 과정이 없기 때문에 빠른 데이터 전송이 가능하다.
2. **적은 오버헤드:** TCP보다 적은 헤더와 연결 관리로 인해 더 가벼워 네트워크 부하가 적다.
3. **멀티캐스팅 및 브로드캐스팅 지원:** 여러 대상에게 동시에 데이터를 전송할 수 있다.

**UDP의 단점:**
1. **신뢰성 부족:** 패킷 손실이나 순서 변경이 발생할 수 있어, 데이터의 정확성을 보장하지 않다. -> 💣 공격자가 해당 서버의 통신 시작 권한을 얻지 않고도 대상 서버에 UDP 트래픽을 폭주시킬 수 있어서 `DDos 공격`에 사용될 위험이 있다
2. **흐름 제어 및 혼잡 제어가 없음:** TCP와는 달리 흐름 제어나 혼잡 제어 기능이 없어서 네트워크 상황에 대한 대처가 어려울 수 있다. 
3. **작은 데이터 크기에 적합:** 큰 데이터 전송이 필요한 경우에는 분할 및 재조립의 추가적인 처리가 필요하다.

### UDP의 체크섬
<figure>
  <img src="http://www.ktword.co.kr/img_data/1796_1.jpg">
  <figcaption>출처: http://www.ktword.co.kr/test/view/view.php?m_temp1=1796</figcaption>
</figure>


UDP의 체크섬은 데이터 무결성을 확인하기 위한 값으로, 데이터 송신 시 패킷의 헤더에 포함되며 **수신 측**에서 오류 여부를 판단하는 데 사용된다.
그러나 오류 감지 후의 복구 기능은 제공하지 않으며, TCP에 비해 높은 전송 속도를 제공하는 대신 신뢰성이 낮은 특성을 가지고 있다.

## 신뢰적 데이터 전송
### UDP는 신뢰성이 낮다고? 데이터는 다 알아서 전송되는거 아닌가요?
정말로 나의 요청이 상대 PC에 정상적으로 도착했는지 100% 신뢰할 수 있을까? <br>
네트워크가 혼잡하거나 중간 노드의 문제, 무선 통신에서의 간섭 등 다양한 요인으로 인해 데이터는 전송되는 동안 손실되거나 유실될 수 있다.<br>
따라서 데이터를 안전하게 주고받기 위해서는 신뢰적인 전송 메커니즘이 필요하다. 

### 그래서 신뢰적 채널이 뭐야?
`신뢰적 채널`은 **데이터 손상과 손실이 없는 것**을 의미한다. 
신뢰적인 채널에서 발생하는 일들을 프로토타입으로 살펴보자. 
신뢰적 데이터 전송(Reliable Data Transfer Protocol) 에 도달하기까지 총 4단계를 거친다
<figure>
  <img src="https://velog.velcdn.com/images/jeongbeom4693/post/f14934d4-d16b-4be5-8e7b-3bd1a7493c9f/image.JPG">
  <figcaption>출처: https://velog.io/@jeongbeom4693/TCP-%EC%8B%A0%EB%A2%B0%EC%84%B1-%EC%9E%88%EB%8A%94-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%A0%84%EC%86%A1%EC%9D%98-%EC%9B%90%EB%A6%AC</figcaption>
</figure>

### 신뢰적 데이터 전송 프로토콜 4단계
#### 1. 완벽하게 신뢰적인 채널 상에서의 신뢰적 데이터 전송 : rdt 1.0
<img src='https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F71YIw%2Fbtq89eopd2h%2Ffhq71KTWJ3er50h99E18QK%2Fimg.jpg'>
<br>

하위 채널이 완전히 신뢰적인 상황이라면 오류가 생길 수 없으므로 수신 측에서는 송신측으로 어떠한 **피드백도 보낼 필요가 없다.** 수신자는 송신자가 데이터를 송신하자마자 데이터를 수신할 수 있기 때문에 **속도를 제어할 필요도 없다.**

#### 2. 비트 오류가 있는 채널 상에서의 신뢰적 데이터 전송 : rdt 2.0
<img src='https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fehc3b6%2Fbtq85CRyTWA%2FKkPXzOtev77Pmnfe1ZVx0k%2Fimg.jpg'>
<br>

다음은 패킷 안의 **비트들이 하위 채널에서 손상**되는 상황이다.<br>
보통 패킷이 전송되거나 버퍼링될 때 네트워크의 물리적 구성요소에서 일반적으로 발생한다. <br>
전송된 모든 패킷은 손실만 있으며 송신된 순서대로 수신된다고 가정한다.<br>

이 때 해결하는 방법은 -> 수신 여부에 따라 **긍정 확인 응답**을 보내거나 수신받지 못한 경우 **부정 확인 응답**을 보내고 **재전송을 요청**한다.<br>

프로토콜 rdt 2.0은 잘 동작할 것 같지만 치명적인 `결함`이 있다.<br>
송신자가 수신자에게 보내는 **ACK/NAK 피드백이 손상되는 경우**를 고려하지 않은 것이다. <br>

예를 들어, 수신 측에서 송신 측으로 ACK 피드백을 보냈는데 이 ACK 패킷이 손상되어 송신 측이 제대로 알아듣지 못한다면 어떻게 해야할까?<br>
=> 송신 측에서 다시 데이터를 보낸다. 그러면 수신 측에서는 데이터를 잘 받았다는 의미로 ACK을 다시 보낼 것이다. <br>
==> 하지만 수신 측에서는 이미 첫번째 데이터에서 잘 받았다고 ACK 피드백을 보냈었는데 똑같은 데이터가 또 온다면 이게 다음 데이터를 의미하는지 **중복**으로 보낸 것인지 알 수가 없다. <br>
이러한 문제 때문에 패킷에 `시퀀스 넘버 (Sequence Number)` 를 포함시킨다.

#### 3. ACK/NAK 피드백이 손상되는 채널 상에서의 신뢰적 데이터 전송 : rdt 2.1, rdt 2.2
<img src='https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc3ES1e%2Fbtq84JKqQCf%2FvXSS78sHNGwamH2g4SnDY0%2Fimg.jpg'>
<img src='https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbu6hAQ%2Fbtq869OTNoC%2FNjXGdu5v3G9RSh7fw8y1e1%2Fimg.jpg'>
<br>

다음은 앞서 잠시 본 것처럼 **ACK/NAK 피드백이 손상**되는 상황이다. <br>
위에서 이러한 문제를 해결하기 위해 `시퀀스 넘버`를 추가한다고 했다. 송신 측은 **0과 1을 시퀀스 넘버로 사용**하고 수신 측은 이 숫자를 통해 수신한 패킷이 새로운 패킷인지 **중복 패킷인지를 판단**한다.<br>
( 새로운 패킷 전송이면 0과 1을 번갈아가며 전송, 재전송인 경우 중복된 시퀀스넘버를 전송한다)<br>

rdt 2.1은 수신 측에서 ACK과 NAK을 모두 응답했다. 하지만 NAK를 보내는 것 대신에 가장 최근에 정확하게 수신된 패킷에 대해서만 ACK를 보내면 이는 NAK을 보낸것과 동일한 의미를 지니게 된다.<br>
따라서 rdt 2.2는 rdt2.1의 기능에서 NAK을 사용하지 않도록 개선되었다.<br>

<img src='https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FPFMvQ%2Fbtq86U4XIQu%2Fy9f6brOxdZUV2iVQOHundk%2Fimg.jpg'>
<img src='https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqP2gf%2Fbtq84uNvxGV%2FUWc5Lwp3KCjOYcChhBSlkk%2Fimg.jpg'>


#### 4. 비트 오류와 손실이 있는 채널 상에서의 신뢰적 데이터 전송 : rdt 3.0
<img src='https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbyDCBW%2Fbtq85CqvDNs%2F8Y7KZl3hs4yejEtZIiSg8k%2Fimg.jpg'>


마지막 상황은 **비트 손상 + 패킷을 손실하는 상황**이다.<br>
패킷이 손실된다면 어떻게 될까? 패킷이 사라졌기 때문에 아무리 기다려도 답이 오지 않을 것이다. <br>
이러한 상황에 대한 해결책으로 송신자 입장에서 최고의 선택은 **패킷을 재전송**하는 것이다. <br>

송신자는 중간에 패킷이 손실이 되던지, 응답이 손실되던지, 단순히 시간이 지연된건지 그 이유를 알지 못하기 때문에 데이터를 **재전송**함으로써 위의 상황들을 한번에 해결할 수 있다. 수신자 입장에서는 시퀀스넘버가 있기 때문에 데이터가 중복되어도 판단이 가능하다.<br>

그렇다면 얼마나 기다렸다가 재전송을 해야할까? -> `카운트다운 타이머`를 이용하여 일정 시간이 지나면 어떤 상황이든 상관없이 패킷을 재전송한다.<br>
<img src='https://github.com/grey920/obsidian_tech-note/assets/58028215/b93f57b8-06fb-45bd-99ba-d80432848aa8'>
<img src='https://github.com/grey920/grey920.github.io/assets/58028215/1dbeb724-fc96-40f2-b59b-debcdcd87cc8'>


rdt 3.0의 출현으로 성능이 눈에 띌 정도로 향상되었지만, 현대적인 고속 네트워크의 요구에는 만족시킬 수 없었다. 그 이유는 신뢰적 데이터 전송이 근본적으로 `전송후 대기 프로토콜`이기 때문이다.

### 전송후 대기 프로토콜 (Stop & wait)
데이터 전송시 송신자가 패킷을 전송하고 수신자의 피드백을 확인하기 전까지 새로운 데이터를 전송하지 않는 것을 `전송 후 대기 프로토콜`이라 한다.<br>

이건 전화 통화하는 상황과 비슷합니다. 상대가 말하면 우리는 ‘어, 응 → 1:ACK’ 또는 ‘뭐라구? → 0:NAK’ 으로 응답하는 상황이라 볼 수 있다. <br>

### 파이프라인 프로토콜
전송 후 대기 프로토콜은 패킷을 한 번 전송 후 다음 패킷을 보내기 위해서는 최소 1RTT(왕복시간) + 패킷전송 시간이 지나야 한다. 이는 **성능면**에서 좋지 않다. 이를 개선하기 위해 파이프라이닝을 통해 **확인 응답을 기다리지 않고 여러 패킷을 전송**한다면 위의 시간을 줄려 좋은 성능을 얻을 수 있다.<br>

하지만 응답을 기다리지 않고 패킷을 전송하게 되면 더 이상 시퀀스 넘버 0과 1을 번갈아 사용할 수 없다. -> 각각의 패킷의 **유일한 시퀀스 넘버**가 필요하다.
<br>

# 출처(참고문헌)
- [HTTP란 무엇입니까?](https://www.cloudflare.com/ko-kr/learning/ssl/what-is-https/)
- [공개키(Public Key) and 개인키(Private Key)](https://blog.naver.com/PostView.naver?blogId=chodahi&logNo=221385524980)
- [DNS란 무엇입니까](https://aws.amazon.com/ko/route53/what-is-dns/)
- [UDP Checksum, TCP Checksum   UDP 체크섬, TCP 체크섬](http://www.ktword.co.kr/test/view/view.php?m_temp1=1796)
- [신뢰적인 데이터 전달 프로토콜의 구축](https://sorjfkrh5078.tistory.com/60)
- [[Network]신뢰적인 데이터 전송과 TCP(1) ](https://frog-in-well.tistory.com/48)

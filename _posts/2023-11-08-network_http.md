---
title: "HTTP 프로토콜"
excerpt: ""
categories:
  - CS
tags:
  - JS 스터디
  - 네트워크
toc: true
toc_sticky: true
toc_label: "HTTP 프로토콜"
toc_icon: "edit"
# classes: wide
header:
  overlay_image: 'https://velog.velcdn.com/images%2Fsdc337dc%2Fpost%2Fd87038b3-e1fb-4de9-bcd2-0930c87f475d%2Fimage.png'
  teaser: 'https://velog.velcdn.com/images%2Fsdc337dc%2Fpost%2Fd87038b3-e1fb-4de9-bcd2-0930c87f475d%2Fimage.png' #/assets/images/2022-01-02/Untitled.png
---
## HTTP 프로토콜이란?
먼저 프로토콜이란 단어를 보자. 
<img width="764" alt="image" src="https://github.com/grey920/grey920.github.io/assets/58028215/c9978c02-17d0-4980-a5c1-dc90f2a12c20">

캠브리지 사전에 등록된 프로토콜이라는 단어를 보면 "공식적인 의식이나 행사에서 사용되는 `규칙`과 허용되는 행동의 체계" 라는 사전적 뜻을 가지고 있다.

`HTTP`는 Hyper Text Transfer Protocol로 그대로 해석하면 하이퍼텍스트를 전송하는 프로토콜이다. 여기서 하이퍼텍스트란 참조(하이퍼링크)를 통해 독자가 한 문서에서 다른 문서로 즉시 접근할 수 있는 텍스트이다.

종합해보면 **하이퍼링크로 연결된 문서 정보를 주고받는 규칙과 체계**라고 볼 수 있겠다. ( HTML 문서 뿐 아니라 다양한 종류의 파일을 전송할 수 있다)

이렇게 웹에서 정보를 주고받는 데 사용되는 프로토콜이기에 웹 브라우징, 웹 검색, 웹 API와 같은 웹 서비스를 구축하고 사용하는 데 중요한 역할을 한다.


## HTTP 프로토콜의 주요 특징

### 요청/응답 모델
<figure>
  <img width="500" alt="image" src="https://developer.mozilla.org/ko/docs/Web/HTTP/Overview/http_request.png">
  <figcaption>출처:https://developer.mozilla.org/ko/docs/Web/HTTP/Overview#http_%EB%A9%94%EC%8B%9C%EC%A7%80</figcaption>
</figure>

<figure>
  <img width="500" alt="image" src="https://developer.mozilla.org/ko/docs/Web/HTTP/Overview/http_response.png">
  <figcaption>출처:https://developer.mozilla.org/ko/docs/Web/HTTP/Overview#http_%EB%A9%94%EC%8B%9C%EC%A7%80</figcaption>
</figure>

HTTP의 파일 전송은 HTTP 요청 (Request)과 응답(Response)를 주고받으면서 이루어진다.
HTTP 요청과 응답의 구조는 서로 닮아 있는데, 그 구조는 다음과 같다.
- 시작 줄에는 실행되어야 할 요청 또는 요청 수행에 대한 성공여부가 담기며, 이 줄은 항상 한 줄로 끝난다.
- 옵션으로 HTTP 헤더가 들어간다. 
- 요청에 대한 모든 메타 정보가 전송되었음을 알리는 빈 줄(blank line)이 삽입된다.
- 요청과 관련된 대용이 옵션으로 들어가거나 응답과 관련된 문서가 들어간다. 본문의 존재 유무 및 크기는 첫 줄과 HTTP 헤더에 명시된다.

#### HTTP Request
웹 브라우저에서 -> 웹 서버 애플리케이션으로 보내는 요청.
HTTP Request는 크게 리퀘스트 라인(시작줄) / 메시지 헤더 / 엔티티 바디 총 세 부분으로 나눈다.

<figure>
  <img width="764" alt="image" src="https://developer.mozilla.org/ko/docs/Web/HTTP/Messages/httpmsgstructure2.png">
  <figcaption>출처: https://developer.mozilla.org/ko/docs/Web/HTTP/Messages</figcaption>
</figure>


- 리퀘스트 라인
	- HTTP Request의 첫 번째 줄로 웹서버에 대한 실제 처리 요청을 전달한다. 항상 **한 줄**로 끝난다.
	- `HTTP 메서드`, `URI (요청 타겟)`,  `버전`으로 구성된다.
		- `HTTP 메서드`는 서버가 수행해야 할 동작을 나타낸다.
		- `요청 타겟`은 주로 URL 또는 프로토콜, 포트, 도메인의 절대 경로로 나타낸다.
		- `HTTP 버전`은 응답 메시지에서 써야 할 HTTP 버전을 알려주는 역할을 한다.
- 메시지 헤더
	- 리퀘스트 라인에 이어지는 여러 줄의 텍스트. 
	- 웹브라우저의 종류와 버전, 대응하는 데이터 형식 등의 정보를 기술한다.
	- 헤더도 Request headers와 General headers, Representation headers로 구분할 수 있다.
  <figure>
    <img width="500" alt="image" src="https://developer.mozilla.org/ko/docs/Web/HTTP/Messages/http_request_headers3.png">
    <figcaption>출처: https://developer.mozilla.org/ko/docs/Web/HTTP/Messages#%ED%97%A4%EB%8D%94</figcaption>
  </figure>
- **공백라인**
- 엔티티 바디
	- 서버로부터 리소스를 가져오는 요청은 보통 본문이 필요없다. (GET, HEAD, DELETE, OPTIONS)
	- 리소스를 업데이트 하기 위해 데이터를 전송하는 경우, 보통 POST 요청으로 데이터를 보낼 때 사용한다.
	- 본문은 크게 단일 리소스 본문과 다중 리소스 본문으로 나눌 수 있다.

#### HTTP Response
웹 서버로부터 -> 웹 브라우저로 요청에 대한 응답을 반환한다.
HTTP Response는 HTTP Request와 유사하게 리스폰스 라인, 메시지 헤더, 엔티티 바디로 구성된다.

- 리스폰스 라인 (status line 상태줄)
	- 리스폰스 라인은 크게 `버전`, `상태 코드`, `설명문`으로 나뉜다.
	- `버전`은 HTTP 버전을 나타내며 현재 주요 버전은 **HTTP/1.1** 프로토콜 버전이다.
	- `상태 코드`는 요청의 성공 여부를 나타내는 3자리로 된 숫자이다. 맨 앞자리에서 대략적인 의미가 정해진다.
	- `설명문`은 사람이 HTTP 메시지를 이해할 수 있도록 상태 코드의 의미를 간단히 보여주는 텍스트이다. 
- 메시지 헤더
	- 웹서버 애플리케이션이 더 자세한 정보를 웹브라우저에 전달하기 위해 이용한다.
	- 예를 들어, 데이터 형식이나 갱신 날짜 등이 기술된다.
  <figure>
    <img width="500" alt="image" src="https://developer.mozilla.org/ko/docs/Web/HTTP/Messages/http_response_headers3.png">
    <figcaption>출처: https://developer.mozilla.org/ko/docs/Web/HTTP/Messages#%ED%97%A4%EB%8D%94_2</figcaption>
  </figure>
- **공백 라인**
- 엔티티 바디
	- 웹 브라우저에 돌려보낼 데이터가 들어간다. ( 주로 HTML 파일 )

### HTTP 메서드
HTTP 메서드는 주어진 **리소스에 수행**하길 원하는 행동을 나타낸다.

|메소드| 의미 |
|---|---|
|GET|URI로 지정한 데이터를 가져온다|
|HEAD| URI로 지정한 데이터의 헤더만 가져온다|
|POST| 서버에 데이터를 보낸다|
|PUT| 요청 payload를 사용해 새 리소스를 생성하거나, 대상 리소스를 대체한다|
|PATCH|리소스의 부분적인 수정을 요청|
|DELETE| 지정한 리소스를 삭제하도록 요청한다|
|CONNECT|요청한 리소스에 대해 양방향 연결을 시작하는 메서드로, 프록시 서버를 경유해 통신한다|

#### PUT과 PATCH의 차이
HTTP PUT 메서드는 전체 리소스를 갱신하는 것만 허용한다. 반면 PATCH 메서드는 리소스의 일부분만 업데이트하는 데 사용된다. 따라서 PUT과 달리 내부 구현에 따라 멱등이 될수도, 멱등이 아닐수도 있다. 
- `멱등하다`는 것은 동일한 **요청을 여러 번** 보내더라도 **동일한 상태 변화**가 발생한다는 것이다. 
- PATCH로  특정 부분만 변경하는 경우 내부에서 추가 연산이 이루어지는 설계가 되어있다면 멱등이 아닐 수 있다. 
	- 예를 들어, { age:10, name: grey} 의 경우 같은 요청을 여러 번 해도 늘 같은 값이 유지될 것이다.
	  하지만 { age:10, name: grey, **operate:add** } 라 하고 operate:add 가 요청될 때마다 age를 +1 씩 증가하는 내부 로직이 있다고 한다면, 같은 요청을 보낼 때마다 age 값은 증가하게 될 것이다. 이는 **멱등하지 않은 것**이다.

#### GET과  POST의 차이
**GET**은 주로 정보를 검색할 때 서버로부터 **데이터를 요청**하여 사용한다. 반면 **POST**는 반대로 양식을 제출하거나 데이터를 새로 생성할 때 서버에 **새로운 데이터를 전송**함으로써 사용한다.


### HTTP 상태코드

| 상태 코드 값|의미|
|---|---|
|1xx|`정보`. 추가 정보가 있음을 전달|
|2xx|`성공`. 서버가 요청을 처리했음을 전달|
|3xx|`리다이렉트`. 다른 URI로 다시 리퀘스트 요청|
|4xx|`클라이언트 에러`. 요청에 문제가 있어 처리할 수 없음을 전달|
|5xx| `서버 에러`. 서버 쪽에 문제가 있어 처리할 수 없음을 전달|

요청이 정상적으로 처리되면 상태 코드로 200을 받는다. 요청이 정상적으로 처리되면 웹 브라우저에는 요청한 내용이 표시되므로 상태코드 200 자체를 사용자가 보게 되는 경우는 거의 없다. 



### HTTP 헤더
HTTP 헤더는 클라이언트와 서버가 요청 또는 응답으로 부가적인 정보를 전송할 수 있도록 한다.
- 구성: 대소문자를 구분하지 않는 이름과 콜론 `:` 다음에 오는 값으로 이루어져있다.

#### 몇 가지 대표적인 헤더
- `Content-Type` 헤더: 
	- 요청이나 응답 본문의 미디어 유형을 나타냅니다. 데이터 형식을 명시하여 클라이언트나 서버가 데이터를 올바르게 해석할 수 있도록 한다. 예시로 JSON 형식의 데이터를 나타내는 경우 **application/json**으로 명시할 수 있습니다.
- `Authorization` 헤더: 
	- 클라이언트가 서버에게 요청을 보낼 때 인증 정보를 포함합니다. 일반적으로 토큰이나 사용자 이름과 암호와 같은 정보를 **인증**하기 위해 사용됩니다.
- `Location` 헤더:
	- 리디렉션 응답에서 새로운 리소스의 위치를 제공합니다. 클라이언트는 이 헤더를 사용하여 다른 페이지로 리다이렉트 하거나 새로운 리소스로 이동할 수 있습니다.
더 다양한 헤더의 설명은 [여기](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers)서 찾아볼 수 있다.

### HTTP의 무상태성(Stateless)
HTTP의 무상태성이란 각 요청이 서로 독립적이며 이전 상태를 공유하지 않는 특성을 의미한다.
요청이 독립적이기 때문에 서버를 스케일 아웃함으로써 부하를 분산시킬 수 있고 웹의 확장성에 도움을 준다.

### HTTP 영속적인 커넥션 (Keep-Alive)
HTTP 기본 동작은 **각 요청마다 새로운 TCP 연결을 생성**하는 것이다(단기 커넥션). 
그리고 TCP 연결을 새로 생성할 때마다 TCP 핸드쉐이크를 수행하고 연결을 설정하고 해제하는 **네트워크 오버헤드**를 가지고 있다. 
`Keep-Alive`는 이 오버헤드를 줄이기 위해 **하나의 TCP 연결**을 여러 요청과 응답이 **재사용**할 수 있도록 허용한다. timeout값과 최대 요청 수를 설정할 수 있고, timeout을 설정하면 이 기간동안만 Connection을 유지하다 서버에서 능동적으로 먼저 연결을 끊는다. 이를 통해 단일 TCP 연결에서 여러 요청과 응답이 이루어지기 때문에 네트워크 지연 시간이 줄어들고 웹 사이트 성능이 좋아진다. HTTP1.1로 와서 keep-alive 기능이 디폴트로 설정되어 있다.

### HTTP 파이프라이닝
기본적으로 HTTP 요청은 순차적이라 현재의 요청에 대한 응답을 받고 나서야 다음 요청을 실시한다. 하지만 네트워크 지연과 대역폭 제한에 걸려 다음 요청을 보내는 데까지 상당한 딜레이가 발생할 수 있다.

`파이프라이닝`이란 같은 Keep-Alive 연결을 통해서 응답을 기다리지 않고 **여러 개의 요청을 하나의 TCP 패킷**으로 연속적으로 패킹해서 보내 커넥션의 지연을 회피하는 기능이다. 이렇게 하면 더 빠른 데이터 전송이 가능하고, 클라이언트와 서버 간의 왕복 시간으로 인한 대기 시간이 줄어들 수 있다.

하지만 정확히 **구현해내기 복잡**하고 **HOL(Head Of Line blocking) 문제**에 영향을 받기 때문에 더 나은 알고리즘인 `멀티플렉싱`으로 대체되었다.

- `HOL 문제`: HTTP1.1까지는 한번에 하나의 파일만 전송이 가능했다. 따라서 여러 파일을 전송할 경우 파이프라이닝은 응답처리를 미루는 방식이므로 각 응답의 처리는 순차적으로 처리되며, 결국 후순위의 응답은 지연될 수 밖에 없다.
- `멀티플렉싱`: HTTP 2.0에서는 여러 파일을 한 번에 병렬로 전송한다.

## HTTP 버전별 특징
### HTTP/1.1 > 표준 프로토콜
1997년 1월에 [RFC 2068](https://datatracker.ietf.org/doc/html/rfc2068)에서 처음 공개된 HTTP의 **첫 번째 표준화 버전**이다. HTTP/1.1에서는 모호함을 명확하게 하고 많은 개선 사항들을 도입했다.
- **연결을 재사용**하여 시간이 절약됨 (Keep-Alive)
- **파이프라이닝**을 추가하여 통신 지연 시간을 단축
- 추가적인 캐시 제어 메커니즘이 도입됨
- 언어, 인코딩, 타입을 포함한 컨텐츠 협상 도입

### HTTP/2 > 더 나은 성능을 위한 프로토콜
시간이 지남에 따라 웹 페이지는 더욱 복잡해졌다. 더 많은 미디어가 표시되고 상호작용을 위한 스크립트 코드의 양도 증가되면서 HTTP 요청도 훨씬 많아졌다. 이를 통해 `HTTP/1.1` 연결에 **복잡성과 오버헤드**가 크게 증가했다. 이를 개선하기 위해 Google은 2010년에 응답성 증가를 정의하고 중복 데이터 전송 문제를 해결한 `SPDY`라는 프로토콜을 구현했고, 이는 `HTTP/2` 프로토콜의 기반이 되었다. HTTP/2 프로토콜은 2015년 5월에 공식적으로 표준화되었다.

- **다중화 프로토콜**. 동일한 연결을 통해 **병렬 요청**을 수행할 수 있어 HTTP/1.x 프로토콜의 제약을 없앰
- **헤더 압축**. 요청 집합 간에 유사한 경우가 많으므로 전송된 데이터의 중복과 오버헤드가 제거된다.
- 서버가 **서버 푸시**라는 메커니즘으로 클라이언트 캐시에 데이터를 저장.

### HTTP/3 > QUIC를 통한 HTTP
HTTP의 다음 주요 버전인 HTTP/3에서는 이전 버전의 HTTP와 동일한 의미를 가지지만, 전송 계층에서 TCP 대신 [`QUIC`](https://developer.mozilla.org/ko/docs/Glossary/QUIC)를 사용한다.

왜 `QUIC` ? 
- HTTP 연결에 대해서 **훨씬 낮은 대기 시간**을 가지도록 설계되었다.
- HTTP/2와 마찬가지로 다중화 프로토콜이지만 `HTTP/2`는 **단일 TCP 연결**을 통해 실행되어 TCP 계층에서 처리되는 패킷 손실 감지 및 재전송이 **모든 스트림을 차단**할 수 있었다. 하지만 `QUIC`는 **UDP**를 통해 **여러 스트림**을 실행하고 각 스트림에 대해 독립적으로 패킷 손실 감지 및 재전송을 구현하므로, 오류가 발생하면 **해당 패킷에 데이터가 있는 스트림만 차단**된다.
HTTP/3는 [RFC 9114](https://datatracker.ietf.org/doc/html/rfc9114)에 정의되어 있다. 
<br>


# 출처(참고문헌)
- [HTTP 메시지](https://developer.mozilla.org/ko/docs/Web/HTTP/Messages)
- 그림으로 배우는 네트워크 원리 - Gene
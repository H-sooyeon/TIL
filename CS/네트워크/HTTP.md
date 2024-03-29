## HTTP(HyperText Transfer Protocol)

인터넷상에서 데이터를 전송하기 위한 프로토콜

TCP/IP 4계층에서 응용계층에 속한다.

응용계층 : OSI 7계층의 응용계층 + 세션 계층 + 표현 계층

- 7계층(`응용 계층`, Application Layer)
  최종 목적지로, 응용 프로세스와 직접 관계하여 일반적인 응용 서비스를 수행한다. (explore, chrome 등)
  `HTTP`, `FTP`, `SMTP`, `POP3`, `IMAP`, `Telnet` 등의 프로토콜을 응용 프로그램의 UI를 통해 제공한다.
- 6계층(`표현 계층`, Presentation Layer)
  데이터를 표준화된 형식으로 변경한다. (데이터 변환, 압축, 암호화 등)
  파일 인코딩, 명령어를 포장, 압축, 암호화
  JPEG, MPEG, GIF, ASCII 등
- 5계층(`세션 계층`, Session Layer)
  세션의 유지 및 해제 등 응용 프로그램 간 통신 제어와 동기화를 한다.
  주 지점간의 프로세스 및 통신하는 호스트 간의 연결을 유지한다.
  TCP/IP 세션 체결, 포트 번호를 기반으로 통신 세션 구성

### HTTP의 특징

1. 비연결성(contextionless)

   TCP/IP와는 달리 클라이언트에서 요청을 보낸 후 서버로부터 응답을 받으면 연결을 끊는 것을 의미한다.

   비연결성은 불특정 다수를 대상으로 하는 서비스에 유리하다.

   연결을 유지하지 않음으로써 자원을 아낄 수 있다.
   하지만 연결을 유지하지 않기 때문에 서버가 클라이언트를 기억할 수 없다는 단점이 있다.

   동일한 클라이언트에서 연속적으로 요청이 오면 연결과 연결 해제 과정을 반복하게 되어 자원을 낭비하게 된다.

   이러한 단점을 보완하기 위해 일정 시간 동안 연결을 유지할 수 있도록 `HTTP Keep Alive`를 사용한다.

   따라서 마지막 응답 이후 일정 시간 동안 연결을 유지해 동일한 클라이언트로부터 요청이 오면 연결 과정을 생략할 수 있다.

   > `HTTP Keep Alive`
   > 클라이언트에서 HTTP 요청을 보낼 때 연결 헤더에 Keep Alive를 추가해서 보내면 서버에서 연결을 유지할 시간을 Keep Alive 헤더에 추가해 응답한다.
   > <br/>

2. 무상태(stateless)

   서버에서 클라이언트의 상태를 저장하지 않는 것을 의미한다.

   클라이언트가 이전에 요청한 사항을 서버에 저장하지 않는다. 따라서 클라이언트는 요청에 필요한 데이터를 모두 가지고 있어야 한다. 또는 서버가 클라이언트로부터 받은 요청 사항을 모두 저장해야 한다.

   이 방법들을 각각 `쿠키(cookie)`와 `세선(session)`이라고 한다.

   무상태의 장점은 서버 확장성이 높다는 점이다.

   클라이언트의 요청에 응답하는 서버가 바뀌어도 되기 때문에 서버를 계속 확장해도 된다. 따라서 특정 서버에 문제가 생겨 응답하지 못하는 문제점을 보완할 수 있다.

   상태일 경우

  <br/>

상태가 유지되어야 하는 프로토콜은 클라이언트A의 요청을 서버1이 기억하고 있기 때문에 항상 서버1이 응답해야 한다.

  <br/>

만약 서버1이 장애가 난다면 유지되던 상태 정보가 다 날아가 버리므로 처음부터 다시 서버에 요청해야 한다.

무상태일 경우

클라이언트A가 요청할 때 필요한 데이터를 다 담아서 보내기 때문에 아무 서버나 호출해도 된다.

  <br/>

만약 서버1에 장애가 생기더라도 다른 서버에서 응답을 전달하면 되기 때문에 클라이언트는 다시 요청할 필요가 없다.

  <br/>

무한한 서버 증설이 가능하다 → DB에서 같은 데이터를 뽑아서 같은 응답을 돌려 줄 수 있다.

> `세션(session)`
> 서버에서 클라이언트와의 연결 정보를 저장 및 관리하는 것을 말한다.
> 서버에 데이터가 저장되므로 보안 면에서는 쿠키보다 좋지만, 접속자가 많을 경우 서버에 과부화가 올 수 있다.

<br/>

HTTP에서는 클라이언트와 서버가 통신하기 위해 정형화된 데이터인 `HTTP 메시지`를 주고받는다.
요청 라인/상태 라인, 헤더, 빈줄, 바디로 이루어진다.<br/>

- 요청 라인(request line): 요청 URI, 요청 방법, HTTP 버전 등을 포함한다.
- 상태 라인(status line): 요청에 대한 HTTP 상태 코드와 HTTP 버전을 포함한다.
- 헤더(header): 키-값으로 구성된 다수의 헤더 항목으로 구성된다.
- 빈 줄(blank line): 헤더의 끝을 나타내는 빈 줄로, 헤더와 바디를 구분한다.
- 바디(body): 요청할 때 요청 방법 메서드가 POST인 경우에만 바디가 있고, 그 외 메서드일 때는 비어 있는 상태로 전달한다.

### HTTP 상태 코드

클라이언트의 요청에 대한 서버의 상태를 알려 주는 코드

1xx: 클라이언트로부터 요청을 받아 처리 중

3xx: 요청을 처리하기 위해 추가 처리 필요

| 상태 코드 | 의미                                   | 분류            |
| --------- | -------------------------------------- | --------------- |
| 200       | 클라이언트 요청을 성공적으로 처리함    | 요청 성공       |
| 401       | 인증되지 않음                          | 클라이언트 오류 |
| 403       | 접근 실패                              | 클라이언트 오류 |
| 404       | 클라이언트에서 요청한 자원을 찾지 못함 | 클라이언트 오류 |
| 500       | 서버 내부 오류 발생                    | 서버 오류       |

## HTTPS

HTTPS(HyperText Transfer Protocal Secure)는 보안 계층인 `SSL/TLS`를 이용해 HTTP의 보안을 강화한 웹 통신 프로토콜이다.

HTTP는 데이터 암호화를 거치지 않고 전송해서 보안에 취약하다.

그래서 이를 보완한 HTTPS가 등장했다.

`SSL(Secure Socket Layer)`은 넷스케이프에서 개발한 암호화 프로토콜이다.

당시 SSL은 몇 가지 문제점이 있었는데, 이를 보완해 새로운 암호화 프로토콜인 `TLS(Transport Layer Security)`를 개발했다. 현재 HTTPS에서 통용되는 방식은 TLS지만, SSL이라는 명칭이 사라지지 않아서 SSL 또는 SSL/TLS 라고 부른다.
<br/>

HTTPS의 동작 방식

데이터를 송신할 때 응용 계층에서 보안 계층의 `SSL/TLS`로 데이터를 보내면 데이터를 암호화해 전송 계층으로 전달한다.

그러면 데이터를 수신할 때 전송 계층에서 보낸 데이터를 보안 계층의 `SSL/TLS`에서 받아 복호화한 후 응용 계층으로 보낸다.

> SSL/TLS 2가지 암호화 방식
> 대칭 키 암호화 방식
> 데이터의 암호화와 복호화에 모두 같은 키인 대칭 키를 이용하는 방식이다.
> 먼저 수신자가 가진 키를 송신자에게 준다.
> 이때 수신자가 같더라도 송신자가 다르면 이용하는 키도 다르다.
> 받은 키로 데이터를 암호화한 후 수신자에게 보낸다.
> 수신자는 동일한 키로 데이터를 복호화한다.

공개 키(비대칭키) 암호화 방식
데이터의 암호화와 복호화를 다른 키로 하는 방식이다.
데이터를 암호화할 때는 공개 키를, 데이터를 복호화할 때는 비밀 키를 이용한다.
먼저 수신자는 공개 키를 송신자에게 준다.
이때 송신자가 달라도 공개 키는 같다. 송신자는 수신자에게 받은 키로 데이터를 암호화한다. 수신자는 비밀 키로 송신자에게 받은 데이터를 복호화한다.
이 방식은 비밀 키가 있어야만 데이터를 복호화할 수 있어서 공개 키 유출을 염려하지 않아도 된다.

>

### 대칭키

암복호화키가 동일하며 해당 키를 아는 사람만이 문서를 복호화해 볼 수 있게 된다.

공개키 암호화 방식에 비해 속도가 빠르다는 장점이 있지만, 키를 교환해야 한다는 문제(키 배송 문제)가 발생한다. 키를 교환하는 중 키가 탈취될 수 있는 문제도 있고 사람이 증가할수록 전부 따로따로 키 교환을 해야하기 때문에 관리해야 할 키가 방대하게 많아진다.

이러한 키 배송 문제를 해결하기 위한 방법으로 키의 사전 공유에 의한 해결, 키 배포센터에 의한 해결, 공개키 암호화에 의한 해결이 있다.

<br/>

### 공개키

대칭키의 키교환 문제를 해결하기 위해 등장한 것이 공개키(비대칭키) 암호화 방식이다.

이름 그대로 키가 공개되어 있기 때문에 키를 교환할 필요가 없어지며 공개키는 모든 사람이 접근 가능하고 개인키는 각 사용자만이 가지고 있는 키이다.

<br/>

1. B 공개키/개인키 쌍 생성
2. 공개키 공개(등록), 개인키는 본인이 소유
3. A가 B의 공개키를 받아옴
4. A가 B의 공개키를 사용해 데이터를 암호화
5. 암호화된 데이터를 B에게 전송
6. B는 암호화된 데이터를 B의 개인키로 복호화 (개인키는 B만 가지고 있기 때문에 B만 볼 수 있음)

공개키는 키가 공개되어 있기 때문에 따로 키 교환이나 분배를 할 필요가 없어진다. 중간 공격자가 B의 공개키를 얻는다고 해도 B의 개인키로만 복호화가 가능하기 때문에 기밀성을 제공하며 개인키를 가지고 있는 수신자만이 암호화된 데이터를 복호화할 수 있으므로 일종의 인증기능도 제공한다는 장점이 있다.

그에 반해 단점은 속도가 느리다는 것이다.

### HTTP와의 차이

1. `https는 제 3자가 봐도 이해할 수 없게 암호화를 시켜 데이터를 주고 받는다.`
   http의 문제점은 내가 전송한 정보를 제 3자가 봤을 때 이해할 수 있는 형식으로 전달된다는 것이었다. 하지만 https에선 http 통신의 body 부분을 암호화해주어 누군가에 의해 탈취당해도 알아볼 수 없도록 해주었다.
2. `신뢰할 수 있는 사이트인지 판별해 준다.` https는 기관에서 검증된 사이트만 허가 받을 수 있다. 그렇기 때문에 url 주소가 유사한 피싱 사이트를 판별하는 데도 도움을 준다.
3. `검색엔진의 SEO 장점을 가진다.` 구글의 검색엔진은 https를 검색 순위 결정 요소에 반영한다.
   https로 더 나은 UX와 사이트 체류 시간 등의 장점을 고려해 반영되어 있다. SEO를 최적화하는데에 있어 HTTPS는 큰 장점을 가진다.

## 웹 페이지 접속 과정

1. 사용자가 URL을 웹 브라우저에 입력한다.
2. 웹 브라우저는 입력한 URL을 바탕으로 `DNS(Domain Name System) 서버`에 연결할 IP를 요청한다.
3. DNS 서버는 IP 주소를 웹 브라우저에게 응답으로 제공한다.
4. 웹 브라우저는 DNS 서버에서 받은 IP를 통해 웹 서버와 TCP/IP 연결을 하고 HTTP 요청을 보낸다.
5. 웹 서버는 받은 HTTP 요청에 응답한다. 응답은 웹 페이지와 필요한 리소스를 포함한다.
6. 웹 브라우저는 받은 응답을 바탕으로 사용자에게 웹 페이지를 보여 준다.

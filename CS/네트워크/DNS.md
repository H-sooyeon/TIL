## DNS

Domain Name Syspem, DNS는 호스트의 도메인네임(www.example.com)을 네트워크주소(IP)로 변환하거나, 그 반대의 역할을 수행하는 시스템이다.

우리가 자주 접하는 naver.com, [google.com](http://google.com) 모두 DNS를 가진 DN(Domain Name)이라고 할 수 있다.

<br />

사용자가 웹브라우저에 도메인 ‘naver.com’을 입력하면 아래와 같은 과정을 거치게 된다.

1. 도메인 주소 naver.com을 브라우저에 입력하게 되면, 도메인 주소들을 가지고 있는 `네임서버`(DNS 서버)에 접속한다.
2. 네임서버에 접속한 도메인(naver.com)과 연결된 IP 정보(223.130.192.200)을 확인하고, IP를 사용자 PC에 전달한다.
3. 사용자 PC는 전달받은 서버의 IP 주소로 접속한다.
4. 서버의 IP로 연결된 브라우저에 서버의 내용을 출력한다.

여기서 DNS 서버에서 도메인과 IP 정보를 얻는 과정이 복잡하게 되어있다.

전세계에 도메인 수가 너무 많기 때문에 DNS 서버 종류를 계층화해서 단계적으로 처리하기 때문이다.

> `Root DNS`(루트 네임서버)
> 인터넷의 도메인 네임 시스템의 루트 존
> ICANN이 직접 관리하는 절대 존엄 서버로, `TLD DNS` 서버 IP들을 저장해두고 안내하는 역할을 한다.
> 전세계에 961개의 루트 DNS가 운영되고 있다.

> `TLD`(최상위 도메인) DNS Server
> TLD는 도메인 등록 기관이 관리하는 서버로, 도메인 네임의 가장 마지막 부분을 말한다. 예를 들어 웹사이트에서 한 번쯤 봤던 .com 이나 [co.kr](http://co.kr) 과 같은 도메인들을 관리하고 부여하는 서버이다.

<br />

1. 웹 브라우저에 www.naver.com을 입력하면 면저 PC에 저장된 Local DNS에게 ‘www.naver.com’이라는 hostname에 대한 IP 주소를 요청한다.
2. Local DNS는 ‘www.naver.com’의 IP 주소를 찾아내기 위해 다른 DNS 서버들과 통신(DNS 쿼리)을 시작한다.
   먼저 Root DNS 서버에게 ‘www.naver.com’의 IP 주소를 요청한다.
3. Loval DNS 서버는 com 도메인을 관리하는 TLD DNS 서버(최상위 도메인 서버)에 다시 www.naver.com에 대한 IP 주소를 요청한다.
4. com 도메인을 관리하는 DNS 서버에도 해당 정보가 없으면, Local DNS 서버에게 www.naver.com의 IP 주소 찾을 수 없음 다른 DNS 서버에게 물어봐 라고 응답을 한다.
5. Local DNS 서버는 [naver.com](http://naver.com) DNS 서버에게 다시 요청한다.
6. [naver.com](http://naver.com) DNS(Authoritative DNS) 서버에는 해당 주소가 있다. Local DNS 서버에게 해당하는 IP 주소를 전달한다.
7. 이를 수신한 Local DNS는 www.naver.com의 IP 주소를 캐싱하고 이후 다른 요청이 있을 시 응답할 수 있도록 IP 주소 정보를 단말(PC)에 전달해준다.

[과정]

Local DNS 서버가 여러 DNS 서버에 차례대로 (Root DNS 서버 → TLD DNS 서버 → Authoritative DNS 서버)요청을 하여 그 답을 찾는 과정을 `재귀적 쿼리(Recursive Query)`라고 부른다.

<br />

Root DNS는 최상위 DNS 서버로 해당 DNS부터 시작해서 아래의 node DNS 서버에게 차례로 물어보게 되는 구조로 짜여져 있다.

즉, 모든 DNS 서버들은 이 Root DNS Server의 주소를 기본적으로 갖고 있다는 말이다.

그래서 모르는 Domain name이 온다면 가장 먼저 Root DNS에게 물어보게 되는 것이다.

하지만 Root DNS Server의 목록에도 해당 Domain Name의 IP 정보가 없다면 다음 DNS 서버로 리턴해주는데, 그 서버가 `TLD(최상위 도메인)서버`이다.

도메인이 google.com이라면 뒤의 문자를 보고 .com을 관리하는 TLD 서버에게 물어보라고 정보를 주는 것이다.

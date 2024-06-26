DNS 요청 과정

1. local DNS 요청
2. Root DNS 요청
3. Top-level DNS 요청
4. Authoriative DNS 요청

<br />

### GSLB (전역 서버 부하 분산)

인터넷 트래픽을 전 세계에 걸쳐 분산된 수 많은 연결된 서버에 배포하는 방식이다.

GSLB의 이점은 향상된 안정성, 대기 시간 감소 등이 있다.

글로벌 특정 지역에 집중되는 트래픽을 분산하는 DNS 기반의 로드밸런싱 기술이다.

DNS 서버는 서버 IP 주소를 매핑 시켜줄 때, 단순 라운드 로빈으로 매핑 시켜주지만, GSLB는 사용자의 IP 주소를 보고 위치기반으로 가장 응답성이 높고 정상 운영중인 서버로 매핑시켜줄 수 있다.

> 글로벌 특정 지역에 트래픽이 증가할 경우에 DNS 기반으로 인접 지역으로 네트워크 트래픽을 자동 분산한다. 특정 서버에 장애가 발생할 경우에는 네트워크 트래픽을 정상 리소스로 로드 밸런싱함으로써 서비스가 안정적으로 지속될 수 있도록 한다.

`로드밸런싱`

애플리케이션을 지원하는 리소스 풀 전체에 네트워크 트래픽을 균등하게 배포하는 방법이다.

최신 애플리케이션은 수백만 명의 사용자를 동시에 처리하고 정확한 텍스트, 비디오, 이미지 및 기타 데이터를 빠르고 안정적인 방식으로 각 사용자에게 반환해야 한다. 이렇게 많은 양의 트래픽을 처리하기 위해 대부분의 애플리케이션에는 데이터가 중복되는 리소스 서버가 많이 있다. `로드 밸런서`는 사용자와 서버 그룹 사이에 위치하며 보이지 않는 촉진자 역할을 하여 모든 리소스 서버가 동일하게 사용되도록 하는 디바이스이다.

<br />

### 부하 분산이란?

둘 이상의 서버 간에 트래픽을 분산하는 방식이다.

- 무작위 DNS 부하 분산 기술
  라운드 로빈 DNS: 각 요청을 지난번 서버와 다른 서버로 보낸다.
- 스마트 부하 분산 기술
  Anycast 라우팅: 부분적으로 클라이언트와 서버간의 가장 빠른 이동 시간을 기반으로 서버를 선택한다.

## IP 프로토콜

인터넷 환경에서 네트워크 계층의 `데이터 전송 프로토콜`로 이용되는 IP(Internet Protocol)는 호스트 주소 표기, 패킷 분할에 관한 기능을 지원하지만, 단대단(end to end) 형식의 오류 제어나 흐름 제어 기능은 제공하지 않는다.

- 비연결 서비스를 제공한다.
- 패킷을 분할/병합하는 기능을 수행하기도 한다.
- 데이터 체크섬은 제공하지 않고, 헤더 체크섬만 제공한다.
- Best Effort 원칙에 따른 전송 기능을 제공한다.

[IP 헤더의 구조]

![Untitled](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F8f34238a-246a-4ffd-8d8a-f3a45a9148ed%2F9091738b-892f-4cb1-9f4d-e2648da839bc%2FUntitled.png?table=block&id=f69c45a8-9813-485b-934a-a5055275cbc8&spaceId=8f34238a-246a-4ffd-8d8a-f3a45a9148ed&width=2000&userId=1b419ea2-181a-44f5-8d9f-c80b349fd635&cache=v2)

상단의 숫자는 비트 수이다.

<br />

### DS/ECN

`차등 서비스` 개념이 도입되면서 Service Type 필드가 6비트의 `DS(Differentiated Service)필드`와 `2비트의 ECN(Explicit Congestion Notification) 필드`로 새로 정의되었다.

이는 인터넷에서 다양한 트래픽 요구 조건을 필요로 하는 서비스들에 대하여 서로 다른 수준의 QoS(Quality of Service)를 지원하기 위함이다.

DS를 사용하기 위해 사전에 서비스 제공자와 서비스 이용자 사이에 서비스 등급에 대한 합의가 이루어지며, 동일한 DS 값을 갖는 트래픽들은 동일한 서비스 등급으로 처리된다.

<br />

### 주소 관련 필드

![Untitled](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F8f34238a-246a-4ffd-8d8a-f3a45a9148ed%2F357c8291-c8cb-4cad-a86b-df7db7e94ade%2FUntitled.png?table=block&id=4a6d9677-9af2-440e-b72b-326285f97ec9&spaceId=8f34238a-246a-4ffd-8d8a-f3a45a9148ed&width=2000&userId=1b419ea2-181a-44f5-8d9f-c80b349fd635&cache=v2)

- `network(네트워크)`
  네트워크 주소이다.
- `host(호스트)`
  네트워크 주소가 결정되면 하위의 호스트 주소를 의미하는 host 비트 값을 개별 네트워크의 관리자가 할당한다.

![Untitled](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F8f34238a-246a-4ffd-8d8a-f3a45a9148ed%2F9091738b-892f-4cb1-9f4d-e2648da839bc%2FUntitled.png?table=block&id=a439edaa-046f-4e8d-adb6-94968e260ffe&spaceId=8f34238a-246a-4ffd-8d8a-f3a45a9148ed&width=2000&userId=1b419ea2-181a-44f5-8d9f-c80b349fd635&cache=v2)

- `Version Number(버전 번호)`
  IP 프로토콜의 버전 번호이다.
- `Header Length(헤더 길이)`
  IP 프로토콜의 헤더 길이를 32비트 워드 단위로 표시한다.
- `Packet Length(패킷 길이)`
  IP 헤더를 포함하여 패킷의 전체 길이를 나타낸다.
- `Time To Live(생존 시간)`
  송신 호스트가 패킷을 전송하기 전에 네트워크에서 생존할 수 있는 시간을 지정하고, 각 라우터에서는 패킷이 지나갈 때마다 필드 값을 감소시키면서 패킷을 중개한다.
  임의의 라우터에서 Time To Live 값이 0으로 감소하면 패킷은 자동으로 버려진다.
- `Transport(전송 프로토콜)`
  IP 프로토콜에 데이터 전송을 요구한 전송 계층의 프로토콜을 가리킨다.

![Untitled](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F8f34238a-246a-4ffd-8d8a-f3a45a9148ed%2F069db044-3c54-4966-b0c4-52b7078c01d7%2FUntitled.png?table=block&id=ce5095a8-e20d-43cf-a367-6d228581bbb2&spaceId=8f34238a-246a-4ffd-8d8a-f3a45a9148ed&width=2000&userId=1b419ea2-181a-44f5-8d9f-c80b349fd635&cache=v2)

- `Header Checksum(헤더 체크섬)`
  전송 과정에서 발생할 수 있는 헤더 오류를 검출하는 기능이다.
- `Options(옵션)`
  네트워크 관리나 보안처럼 특수 용도로 이용할 수 있다.
- `Padding(패딩)`
  IP 헤더의 크기는 16비트 워드의 크기가 4의 배수가 되도록 설계되어 있다. 필드의 전체 크기가 이 조건에 맞지 않으면 이 필드를 사용해 조정할 수 있다.

## NoSQL

`Not only SQL` 혹은 `Non-Relational Operational DataBase`의 약자로 비관계형 데이터베이스를 지칭한다.

기존의 RDBMS와 같은 관계형 데이터 모델을 지양하며 대량의 분산된 데이터를 저장하고 조회하는데 특화된 데이터베이스로 스키마 없이 사용하거나 느슨한 스키마를 제공하는 저장소이다.

→ 주로 빅데이터, 분산 시스템 환경에서 대용량의 데이터를 처리하는데 적합하다.

즉, 기존의 RDBMS가 `Consistency`와 `Availability`에 중점을 두었다면 NoSQL은 `Scalability`와 `Availability` (유효성)에 중점을 두고 있다.

<br />

## NoSQL의 특징

- RDBMS와 달리 데이터 간의 관계를 정의하지 않는다.
  RDBMS는 데이터 간의 관계를 Foreign Key로 정의하고 Join 연산을 수행할 수 있지만, NoSQL은 `key-value` 형태로 저장되기 때문에 join 연산이 불가능하다.
- RDBMS에 비해 대용량의 데이터를 저장할 수 있다.
- 분산형 구조로 설계되어 있다.
  여러 곳의 서버에 데이터를 분산 저장하여 특정 서버에 장애가 발생했을 때도 데이터 유실 혹은 서비스 중지가 발생하지 않도록 한다.
- 고정되어 있지 않은 테이블 스키마를 갖는다.
  RDBMS와 달리 테이블의 스키마가 유동적이고 데이터를 저장하는 컬럼이 각기 다른 이름과 다른 데이터 타입을 갖는 것이 허용된다.
- 키 값이 중복될 수 있기 때문에 키 값을 잘 설계해야 한다.

<br />

## NoSQL 장단점

### 장점

- RDBMS에 비해 저렴한 비용으로 분산처리와 병렬 처리가 가능하다.
- 비정형 데이터 구조 설계로 설계 비용이 감소한다.
- big data 처리에 효과적이다.
- 가변적인 구조로 데이터 저장이 가능하다.
- 데이터 모델의 유연한 변화가 가능하다.

<br />

### 단점

- 데이터 업데이트 중 장애가 발생하면 데이터 손실 발생 가능
- 많은 인덱스를 사용하려면 충분한 메모리가 필요하며 인덱스 구조가 메모리에 저장된다.
- 데이터 일관성이 항상 보장되지 않는다.

→ 즉, 최종적 일관성(Eventually Consistent)을 지향한다.

> 데이터 변경이 발생했을 때, 시간이 지남에 따라 여러 노드에 전파되면서 당장은 아니지만 **최종적**으로 **일관성**이 유지되는 것을 `최종 **일관성**(Eventual Consistency)`이라고 한다.

NoSQL 종류

Redis, Oracle NoSQL DB, MongoDB, Hbase 등

- key-value database
- wide-column database
- document database
- graph database

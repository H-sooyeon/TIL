### 데이터 조작어 (DML)

`Data Manipulation Language`

- `SELECT`
  데이터베이스에 들어있는 데이터를 조회하거나 검색하기 위한 명령어
- `INSERT`, `UPDATE`, `DELETE`
  데이터베이스의 테이블에 들어있는 데이터에 변형을 가하는 종류(데이터 삽입, 수정, 삭제)의 명령어

### 데이터 정의어 (DDL)

`Data Definition Language`

- `CREATE`, `ALTER`, `DROP`, `RENAME`, `TRUNCATE`
  테이블과 같은 데이터 구조를 정의하는데 사용되는 명령어들로(생성, 변경, 삭제, 이름 변경) 데이터 구조와 관련된 명령어
  `CREATE`: 데이터 베이스, 테이블 등을 생성하는 역할

      `ALTER`: 테이블을 수정하는 역할

      `DROP`: 데이터베이스, 테이블을 삭제하는 역할

      `TRUNCATE`: 테이블을 초기화 시키는 역할

### 데이터 제어어 (DCL)

`Data Control Language`

- `GRANT` , `REVOKE` , `ROLLBACK`, `COMMIT`
  데이터베이스에 접근하고 객체들을 사용하도록 권한을 주고 회수하는 명령어
  데이터베이스 관리자는 데이터베이스에 대한 접근 권한을 갖지 못한 사용자로부터 데이터를 안전하게 보호할 의무가 있다. 데이터의 보안, 무결성, 회복, 수행제어 등을 정의하는데 사용한다.

      `GRANT`: 사용자에게 권한을 부여하는 명령어

      `REVOKE`: 사용자로부터 권한을 삭제하는 명령어

      `COMMIT`: 트랜잭션의 작업 결과를 반영

      `ROLLBACK`: 트랜잭션의 작업을 취소 및 원래대로 복구

### 트랜잭션 제어어 (TCL)

`Transaction Control Language`

- `COMMIT`, `ROLLBACK`
  논리적인 작업의 단위를 묶어서 DML에 의해 조작된 결과를 작업단위(트랜잭션) 별로 제어하는 명령어
  DCL에서 트랜잭션을 제어하는 명령인 COMMIT, ROLLBACK만을 따로 분리해서 표현한다.

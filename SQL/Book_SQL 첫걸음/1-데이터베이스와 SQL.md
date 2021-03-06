# 1. 데이터베이스와 SQL

## 2020.10.01

### 1-1. 데이터베이스

#### 데이터베이스 (DB: Database)
- 비휘발성 저장장치에 저장되는 영속된 데이터의 집합
- 특정 데이터를 확인하고 싶을 때 간단하게 검색할 수 있도록 정리된 형태
- 데이터베이스는 다양한 시스템(웹 시스템, POS시스템, 휴대전화 등등)에서 사용

#### 데이터베이스 관리 시스템 (DBMS: Database Management System)
- 데이터베이스를 효율적으로 관리하는 소프트웨어
- 사용 목적은 생산성 향상, 기능성과 신뢰성 확보

#### SQL
- 관계형 데이터베이스 관리 시스템 (**RDBMS**: Relational Database Management System)**을 조작할 때 사용하는 표준 언어**
- SQL에는 제품의 경우에 따라 방언이 존재하지만, 방언 대신 표준 SQL을 사용하는 것이 좋음
- SQL명령의 종류
  - DML (Data Manipultation Language) : 데이터를 조작할 때 사용하는 SQL의 가장 기본이 되는 명령셋
  - DDL (Data Definition Language) : 데이터를 정의하는 명령어
  - DCL (Data Control Language) : 데이터를 제어하는 명령어


### 1-2. 다양한 데이터베이스

#### 데이터베이스 종류
오래된 순서로
- 계층형 데이터베이스 : 폴더와 파일 등의 계층 구조로 데이터를 저장하는 방식
- **관계형 데이터베이스** : 행과 열을 가지는 표 형식 데이터를 저장하는 형태 (2차원 데이터), **SQL명령어 사용**
- 객체지향 데이터베이스 : 가능하면 객체 그대로를 데이터베이스의 데이터로 저장하는 것
- XML 데이터베이스 : XML 형식으로 기록된 데이터를 저장하는 데이터베이스로 XQuery명령어 사용
- 키-밸류 스토어(KVS) : 키와 그에 대응하는 값이라는 단순한 형태의 데이터를 저장하는 데이터베이스

#### RDBMS 제품
- Oracle
- DB2
- SQL Server
- PostgreSQL
- MySQL
- SQLite


### 1-3. 데이터베이스 서버
  
#### 클라이언트/서버 모델
- 많은 **RDBMS는 클라이언트/서버 모델로 구성**
- 사용자 조작에 따라 요청을 전달하는 '클라이언트'와 해당 요청을 받아 처리하는 '서버'로 소프트웨어를 나누고, 복수의 컴퓨터 상에서 하나의 모델을 구현하는 시스템
- 유연한 하드웨어 구성을 실현
- 웹 시스템에서의 클라이언트/서버
  - 브라우저와 웹 서버로 구성
  - 브라우저가 URL을 통해 웹 서버에 어떠한 요청을 하면, 웹 서버는 알맞은 처리 후 응답
- RDBMS의 클라이언트/서버
  - 데이터베이스에 접속하기 위해서는 사용자 ID와 비밀번호를 이용한 **사용자 인증 필요**
  - RDBMS에 접속하면, 클라이언트에서 SQL명령을 서버에 보내고 응답을 받음

#### 웹 애플리케이션의 구조
- 일반적으로 웹 서버와 데이터베이스 서버의 조합으로 구축
- 웹 서버에서 동적 콘텐츠를 생성하기 위해 CGI를 이용
  - 실제로 데이터베이스에 접속하는 것은 CGI 프로그램
  - CGI 프로그램이 데이터베이스의 클라이언트 역할
- 클라이언트 브라우저에서 웹 서버로 요청을 보내면 -> CGI프로그램이 DB에 접속하여 SQL명령을 전달하고 -> DB에서 실행 결과를 다시 CGI프로그램으로 보내주면 -> CGI프로그램이 받은 실행 결과를 이용하여 동적으로 HTML을 생성하여 -> 그 결과물을 웹 서버가 클라이언트 브라우저에게 응답

#### MySQL 서버와 mysql 클라이언트
- MySQL 서비스가 데이터베이스 서버, mysql 커맨드가 클라이언트
- PC 한 대로 서버와 클라이언트 모두 실행 가능
- 클라이언트에서 서버에 접속할 때 네트워크를 경유해서 PC 서버로 되돌아오는 '루프 백 접속' 형태를 사용하므로 네트워크 기능은 필요

<br>

### Reference
- [SQL 첫걸음](http://www.yes24.com/Product/Goods/22744867?OzSrank=1) - 아사이 아츠시 저. 한빛미디어. 2015
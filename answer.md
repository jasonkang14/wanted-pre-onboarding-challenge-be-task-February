1. 관계형 데이터베이스(RDBMS)와 비관계형 데이터베이스(NoSQL)의 장단점 비교

[SQL]
데이터는 정해진 데이터 스키마에 따라 테이블에 저장됨.
데이터는 관계를 통해 여러 테이블에 분산됨.

데이터는 테이블에 레코드로 저장되는데, 각 테이블마다 명확하게 정의된 구조가 있음.
해당 구조는 필드의 이름과 데이터 유형으로 정의됨.
따라서 스키마를 준수하지 않은 레코드는 테이블에 추가할 수 없음.
스키마를 변경하지 않는 이상은 정해진 구조에 맞는 레코드만 추가할 수 있음.
관계를 맺고 있는 데이터가 자주 변경되는 애플리케이션의 경우
변경될 여지가 없고, 명확한 스키마가 사용자와 데이터에게 중요한 경우

* 장점
명확하게 정의된 스키마, 데이터 무결성 보장
관계는 각 데이터를 중복없이 한번만 저장

* 단점
덜 유연함. 데이터 스키마를 사전에 계획하고 알려야 함. (나중에 수정하기 힘듬)
관계를 맺고 있어서 조인문이 많은 복잡한 쿼리가 만들어질 수 있음
대체로 수직적 확장(CPU 업그레이드 등을 통한 단순히 DB 서버의 성능을 향상)만 가능함

[No SQL]
레코드 = Documents
다른 구조의 데이터를 같은 Collection에 추가할 수 있음.
Documents는 JSON과 비슷한 형태.
RDBMS처럼 여러 Table에 나누어 담지 않고, 관련 데이터를 동일한 Collection에 넣음.
따라서, Join할 필요 X
Join을 잘 사용하지 않고 자주 변경되지 않는 데이터일 때 효율적.
정확한 데이터 구조를 알 수 없거나 변경/확장 될 수 있는 경우
읽기를 자주 하지만, 데이터 변경은 자주 없는 경우
데이터베이스를 수평으로 확장해야 하는 경우 (막대한 양의 데이터를 다뤄야 하는 경우)

* 장점
스키마가 없어서 유연함. 언제든지 저장된 데이터를 조정하고 새로운 필드 추가 가능.
데이터는 애플리케이션이 필요로 하는 형식으로 저장됨. 데이터 읽어오는 속도 빨라짐.
수직 및 수평 확장이 가능해서 애플리케이션이 발생시키는 모든 읽기/쓰기 요청 처리 가능

* 단점
유연성으로 인해 데이터 구조 결정을 미루게 될 수 있음.
데이터 중복을 계속 업데이트 해야 함.
데이터가 여러 컬렉션에 중복되어 있기 때문에 수정 시 모든 컬렉션에서 수행해야 함 (SQL에서는 중복 데이터가 없으므로 한번만 수행이 가능)


2. 트랜잭션(transaction)이란 무엇인가요

https://d2.naver.com/helloworld/407507

하나의 논리적 작업 단위를 구성하는 일련의 연산들의 집합


3. MySQL에서 조인(join)의 역할은 무엇인가요? 다양한 join의 방식에 대해 설명해주세요.
두 개 이상의 테이블이나 데이터베이스를 연결하여 데이터를 검색하는 방법

- #### INNER JOIN

  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile9.uf.tistory.com%2Fimage%2F99799F3E5A8148D7036659">

  교집합

  <br>

- #### LEFT OUTER JOIN

  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile6.uf.tistory.com%2Fimage%2F997E7F415A81490507F027">

  <br>

- #### RIGHT OUTER JOIN

  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile25.uf.tistory.com%2Fimage%2F9984CE355A8149180ABD1D">

  <br>

- #### FULL OUTER JOIN

  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile24.uf.tistory.com%2Fimage%2F99195F345A8149391BE0C3">
  
  합집합

  <br>

- #### CROSS JOIN

  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile10.uf.tistory.com%2Fimage%2F993F4E445A8A2D281AC66B">
  
  모든 경우의 수
  A가 3개, B가 4개면 총 3*4 = 12개의 데이터

  <br>

- #### SELF JOIN

  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile25.uf.tistory.com%2Fimage%2F99341D335A8A363D0614E8">

  자기자신과 자기자신을 조인
  자신이 갖고 있는 칼럼을 다양하게 변형시켜 활용할 때 자주 사용


4. MySQL에서 인덱스(index)란 무엇인가요?

DB 테이블의 검색 속도를 향상시키기 위한 자료구조.
해당 Table의 Recod를 Full Scan 하지 않고 Index 파일을 검색하여 검색속도를 빠르게 함.
B+ Tree 구조에서 Index 파일 검색으로 속도를 향상시키는 기술

Table 생성 시, 3개의 파일이 생성됨
FRM : Table 구조 저장 파일
MYD : 실제 Data 파일
MYI : Index 정보 파일(Index 사용 시 생성) 

사용자가 Query를 통해 Index를 사용하는 Column을 조회했을 경우, MYI 파일을 활용.
Select Query의 Where절, Join 예약어를 사용했을 때만 Index 사용됨.
PK나 Unique 제약 조건을 정의한 경우 Unique Index가 자동으로 생성됨.
Index를 사용하는 Column은 다른 형태로 가공해서 사용하면 적용되지 않음. (필요 시, 함수 기반 Index 사용)

단점
.mdb 파일 크기가 증가
여러 사용자 응용 프로그램에서의 여러 사용자가 한 페이지를 동시에 수정하는 병행성이 줄어듬 (?)
Index 된 Field에서 Data를 Insert, Delete, Update 시 재작성해야되서 성능이 떨어짐.
Data 중복도가 높은 Column, DML이 자주 일어나는 Column X
10% 내외 공간 추가로 필요

## 목차
- [1번 문제](#1-관계형-데이터베이스rdbms와-비관계형-데이터베이스nosql의-장단점-비교)
- [2번 문제](#2-트랜잭션transaction이란-무엇인가요)
- [3번 문제](#3-mysql에서-조인join의-역할은-무엇인가요-다양한-join의-방식에-대해-설명해주세요)
- [4번 문제](#4-mysql에서-인덱스index란-무엇인가요)

<br/>

### 1. 관계형 데이터베이스(RDBMS)와 비관계형 데이터베이스(NoSQL)의 장단점 비교
> 관계형 데이터베이스  
> 데이터가 하나 이상의 열과 행의 테이블(관계)에 저장되어 서로 다른 데이터 구조가 어떻게 관련되어 있는지 쉽게 파악하고 이해할 수 있도록 사전 정의된 관계로 데이터를 구성하는 정보 모음

> 비관계형 데이터베이스  
> 관계형 데이터베이스보다 덜 제한적인 일관성 모델을 이용해 데이터를 구성하는 정보 모음

<br/>

||RDBMS|NoSQL|
|:---:|:---|:---|
|장점|명확하게 정의된 스키마<br/>데이터 무결성 보장|데이터 스키마가 없어 유연<br/>애플리케이션이 필요한 형태로 데이터 저장<br/>수직 및 수평적 확장 가능|
|단점|사전 정의된 스키마 사용으로 덜 유연<br/>데이터 조회 시 복잡한 쿼리 생성 가능<br/>대체로 수직적 확장만 가능|데이터 구조 결정을 미룰 수 있음<br/>중복 데이터 수정 시 모든 컬렉션 업데이트 필요|
|사용처|명확한 스키마가 중요한 경우<br/>데이터가 자주 변경되는 경우|정확한 데이터 구조를 알 수 없거나 변경될 수 있는 경우<br/>데이터의 변경은 자주 없는 경우<br/>막대한 양의 데이터를 다루는 경우|

<br/>

### 2. 트랜잭션(transaction)이란 무엇인가요?
> 트랜잭션  
> 데이터베이스 상태를 변화시키는 하나의 논리적 작업 단위  
> 작업이 하나라도 실패하면 전부 수행 실패, 작업이 모두 성공해야 수행 성공

- 트랜잭션 특징: 안전한 트랜잭션 수행을 위한 성질
    1. 원자성, Atomicity: 모든 연산이 완벽히 수행되어야하며 하나의 연산이라도 실패하면 트랜잭션 실패
    2. 일관성, Consistency: 데이터가 유효한 상태로만 변경 가능
    3. 고립성, Isolation: 동시에 실행될 경우 다른 트랜잭션에 영향을 받지 않고 독립적으로 실행
    4. 내구성, Durability: 커밋 이후에 시스템 오류가 발생하더라도 커밋된 상태로 유지되는 것 보장

- 트랜잭션 격리 수준
    - 동시에 여러 트랜잭션이 처리될 때, 특정 트랜잭션이 다른 트랜잭션에서 변경하거나 조회하는 데이터를 볼 수 있도록 혀용할지 말지 결정하는 것
    - READ UNCOMMITTED - READ COMMITTED - REPEATABLE REAd - SERIALIZABLE 순서대로 격리 수준이 높음

- 트랜잭션 격리 수준 설정 및 조회
```sql
# MYSQL
SHOW VARIABLES LIKE '%isolation';
SET [GLOBAL | SESSION] TRANSACTION transaction_characteristic [, transaction_characteristic] ...;

/*
# transaction_characteristic
ISOLATION LEVEL [level | access_mode]
*/
```

<br/>

### 3. MySQL에서 조인(join)의 역할은 무엇인가요? 다양한 join의 방식에 대해 설명해주세요.
> JOIN  
> 데이터베이스 내 여러 테이블에서 가져온 레코드를 조합해 하나의 테이블 결과로 표현할 수 있는 키워드

- JOIN 종류
    1. INNER JOIN: ON 조건식에 만족하는 1st, 2nd 테이블의 교집합
    ```sql
    SELECT * 
    FROM {1st 테이블명} [INNER] JOIN {2nd 테이블명} ON {1st 테이블 비교필드} = {2nd 테이블 비교필드}
    [WHERE {조건식}];
    ```
    2. LEFT JOIN: ON 조건식에 만족하지 않는 필드의 경우 1st 테이블의 값은 모두 사용, 2nd 테이블의 해당 필드 값 null
    ```sql
    SELECT * 
    FROM {1st 테이블명} LEFT JOIN {2nd 테이블명} ON {1st 테이블 비교필드} = {2nd 테이블 비교필드}
    [WHERE {조건식}];
    ```
    3. RIGHT JOIN: ON 조건식에 만족하지 않는 필드의 경우 2nd 테이블의 값은 모두 사용, 1st 테이블의 해당 필드 값 null
    ```sql
    SELECT * 
    FROM {1st 테이블명} RIGHT JOIN {2nd 테이블명} ON {1st 테이블 비교필드} = {2nd 테이블 비교필드}
    [WHERE {조건식}];
    ```
    4. NATURAL JOIN: 두 테이블의 같은 필드명의 같은 필드값을 가진 데이터가 있을 경우 동작
    ```sql
    SELECT * 
    FROM {1st 테이블명} NATURAL JOIN {2nd 테이블명};
    ```
    5. CROSS JOIN: 두 테이블의 모든 행이 연결되는 모든 데이터 조합
    ```sql
    SELECT * 
    FROM {1st 테이블명} CROSS JOIN {2nd 테이블명};
    ```
    6. SELF JOIN: 자기 자신을 하나씩 비교해 데이터 조합
    ```sql
    SELECT * 
    FROM {테이블명} AS {1st 별칭} [INNER] JOIN {테이블명} AS {2nd 별칭} ON {1st 별칭.비교필드} = {2nd 별칭.비교필드}
    [WHERE {조건식}];
    ```

<br/>

### 4. MySQL에서 인덱스(index)란 무엇인가요?
> INDEX  
> 테이블에서 원하는 데이터를 쉽고 빠르게 찾기 위해 사용  
> 검색에 자주 사용되는 필드 값으로 만들어진 원본 테이블의 사본

- 장점
    - 테이블 전체를 읽지 않아도 되므로, 검색과 질의에 대한 처리가 빠르게 이루어짐

- 단점
    - 사용자가 직접 접근할 수 없음
    - 인덱스가 설정된 필드 값을 포함한 데이터의 삽입, 삭제, 수정이 이루어질 경우 인덱스도 업데이트 필요
    - 인덱스가 설정된 테이블이 수정될 경우 처리 속도가 느려질 수 있음

- INDEX 설정 및 조회
    ```sql
    SHOW INDEX FROM {테이블명};
    CREATE [UNIQUE] INDEX {인덱스명} ON {테이블명} ({필드명, ...} [DESC | ASC]);
    ALTER TABLE {테이블명} ADD [UNIQUE | FULLTEXT] INDEX {인덱스명} ({필드명, ...});
    ALTER TABLE {테이블명} DROP INDEX {인덱스명}; | DROP INDEX {인덱스명} ON {테이블명};
    ```

<br/>

**★ INDEX 조금 더 상세히 알아보는 시간 가지기 ★**

#### References
@http://www.tcpschool.com/mysql/mysql_index_create
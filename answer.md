## 1. 관계형 데이터베이스(RDBMS)와 비관계형 데이터베이스(NoSQL)의 장단점 비교

### 관계형 데이터베이스의 장점
* 정규화된 데이터 구조
  * 정규화란 관계형 데이터베이스에서 중복을 최소화하기 위한 데이터의 구조를 결정하는 작업을 말한다.
  * 정규화를 통해 서로 관련있는 속성들로만 릴레이션을 구성하여 이상 현상을 방지할 수 있다.
* 높은 데이터 안정성


### 관계형 데이터베이스의 단점
* 스키마에 제약이 있다.
  * 여러 테이블이 서로 관계를 맺고 있기 때문에 기존에 작성되어 사용중인 테이블을 수정하게 되면 여러 테이블에서 영향을 받게 된다.
* 비정규화 데이터 구조에 적합하지 않다.
* 대용량 데이터에서 성능 저하 우려가 있다.
  * 인덱스가 제대로 작동한다면 대용량 데이터에서도 성능 저하가 발생하진 않지만, 복수의 JOIN을 수행하면서 네스티드 루프가 발생하면 RDB의 성능 저하가 발생할 수 있다.

### NoSQL 데이터베이스(Not Only SQL)의 장점
* 스키마가 유연하여 언제든지 새로운 필드를 추가할 수 있다.
* 분산환경에서 데이터를 분산하기에 용이하여 확장성이 좋다.
  * rdb는 데이터의 중복을 최소화하는 대신 테이블간 관계를 맺는 식으로 사용하기 때문에 scale out이 어렵다. 하지만 NoSQL은 관계를 맺지 않고 특정 컬렉션에 모든 데이터를 저장하고 있기 때문에 데이터를 나눠서 저장해도 문제가 없다. 때문에 scale out이 용이하다.
* 위와 같은 이유로 대용량 데이터 처리 및 대규모 트래픽을 처리하기에 적합하다.

### NoSQL 데이터베이스의 단점
* 쿼리 성능이 제한적
  * but 애초에 쿼리 프로세싱을 간단하게 하고 데이터를 중복 저장하도록 함.
* 데이터 안정성 저하
  * 트랜잭션을 지원하지 않으므로 데이터의 일관성이 떨어진다.
* 표준화가 미흡.

<br>

RDB와 NoSQL 둘 다 단점이 장점이 되기도 하고, 장점이 단점이 되기도 하는 것 같다. 즉 상황에 맞춰 무엇을 사용할지 선택해야 한다는 것.


## 2. 트랜잭션(transaction)이란 무엇인가요?

###  트랜잭션이란
* db의 상태를 변화시키는 하나의 논리적인 작업 단위.
* 하나의 트랜잭션 내에는 여러 개의 연산이 수행될 수 있으며, 그중 하나라도 작업이 실패하면 트랜잭션 자체가 실패한다.

### ACID
* 데이터베이스 트랜잭션이 안정적으로 수행된다는 것을 보장하기 위한 성질을 가리키는 용어이다
#### 원자성(Atomicity)
  * 하나의 트랜잭션과 관련된 작업들이 수행될 거면 모두 수행되고, 아니면 모두 수행되지 않을 것을 보장하는 성질.
  * 트랜잭션의 작업 중 일부분만 성공되는 경우는 있을 수 없다. 결제 단계가 중간에서 실패하면 관련 작업을  모두 되돌려야 하는 게 맞는 것처럼.
#### 일관성(Consistency)
  * 트랜잭션이 수행된 이후에도 데이터베이스가 이전과 같이 유효한 상태여야 한다는 것.
  * 트랜잭션이 일어난 후의 데이터베이스가 데이터베이스의 제약이나 규칙을 만족해야 한다.
    * 예를 들어 어느 트랜잭션으로 묶인 일련의 작업 과정에서 어떤 테이블에 외래키를 설정하여 데이터를 삽입하려고 하는데, 참조하려는 테이블에 기본키로 선언되어있지 않은 데이터를 삽입할 수 없다(참조 무결성 제약조건).
#### 고립성(Iscolation)
  * 어떤 트랜잭션이 수행되고 있는 중에는 다른 트랜잭션이 중간에 개입해서 영향을 주지 못하도록 하는 성질.
  * 동시성 제어 관련
#### 지속성(Durability)
  * 트랜잭션이 성공한 후에는 데이터베이스에 반영된 결과가 영원히 반영되어야 한다는 것.
  *  트랜잭션 정상 완료 후에는 버퍼의 내용을 하드디스크(데이터베이스)에 확실히 기록하여야 하며, 부분 완료된 경우에는 작업을 취소하여야 한다.

### 트랜잭션 격리수준
* 동시에 여러 트랜잭션이 처리될 때, 트랜잭션끼리 서로 얼마나 고립되어있는지를 나타내는 정도.
* 특정 트랜잭션이 다른 트랜잭션에서 변경한 데이터를 볼 수 있도록 허용할지 말지를 결정하는 정도.
* 트랜잭션 격리수준은 고립도와 성능의 트레이드 오프를 조절한다.

#### READ UNCOMMITED
- 다른 트랜잭션에서 커밋되지 않은 내용도 참조 가능.
- 데이터 정합성에 문제가 많음(동시성 문제).
#### READ COMMITED
- 어떤 트랜잭션에서 변경된 내용이 커밋되어야만 다른 트랜잭션에서 참조할 수 있다.
#### REPEATABLE READ
- 트랜잭션에 진입하기 이전에 커밋된 내용만 참조할 수 있다.
#### SERIALIZABLE
- 트랜잭션에 진입하면 락을 걸어 다른 트랜잭션이 접근하지 못하게 한다.
- 성능이 매우 떨어진다.


## 3. MySQL에서 조인(join)의 역할은 무엇인가요? 다양한 join의 방식에 대해 설명해주세요.

### JOIN이란
* 둘 이상의 테이블 사이에서 연관된 column을 기반으로 row를 결합하는 기능입니다.

### JOIN의 종류

### 1. INNER JOIN

- **두 테이블의 교집합**. JOIN 조건을 만족하는 행을 반환한다.
- 그냥 JOIN만 적어줄 시 기본적으로 INNER JOIN이 실행된다.

```sql
SELECT *
FROM table1
INNER JOIN table2
ON table1.id = table2.id;
```

```sql
SELECT * 
FROM table1, table2
WHERE table1.id = table2.id
```

### 2. OUTER JOIN

- **조인 조건에서 동일한 값이 없는 행도 반환**할 때 사용한다.
    
    ### 2-1 LEFT OUTER JOIN
    
    - 조인문의 왼쪽에 있는 테이블의 모든 결과를 가져온 후 오른쪽 테이블의 데이터를 매칭하고, 매칭되는 데이터가 없는 경우 NULL을 표시한다.
    - 쉽게 말해서 양쪽 테이블에서 공통되는 데이터(A ∩ B)에 + FROM절 테이블에만 존재하는 데이터(A - B)를 추가한다.
    - `LEFT JOIN` 이라고만 해도 `LEFT OUTER JOIN` 이 실행된다.
    
    ```sql
    SELECT *
    FROM table1 t1
    LEFT OUTER JOIN table2 t2
    ON t1.id = t2.id;
    ```
    
    ### 2-2 RIGHT OUTER JOIN
    
    - left outer join의 반대
    
    ```sql
    SELECT *
    FROM table1 t1
    RIGHT OUTER JOIN table2 t2
    ON t1.id = t2.id;
    ```
    
    ### 2-3 FULL OUTER JOIN
    
    - LEFT OUTER JOIN과 RIGHT OUTER JOIN을 합친 것.
    - 양쪽 모두 조건이 일치하지 않는 것까지 모두 결합하여 출력한다.
    - 매칭되는 데이터가 없는 경우 NULL을 표시한다.
    
    ```sql
    SELECT *
    FROM table1 t1
    FULL OUTER JOIN table2 t2
    ON t1.id = t2.id;
    ```
    

### 3. CROSS JOIN

- **카테시안 곱**. 곱집합을 반환한다.

```sql
SELECT * 
FROM TABLE1
CROSS JOIN TABLE2;
```

### 4. NATURAL JOIN

- 두 테이블에서 컬럼명이 동일하고, 컬럼의 자료형, 값이 같은 행을 반환한다.

```sql
SELECT * 
FROM table1
NATURAL JOIN table2;
```

### JOIN에서 USING과 ON의 차이

- USING절은 ON절과 마찬가지로 JOIN 조건을 설정할 때 사용한다.

```sql
SELECT *
FROM table1
JOIN table2
USING (name, gender); -- 괄호 필수

SELECT *
FROM table1 t1
JOIN table2 t2
ON t1.name = t2.name
AND t1.gender = t2.gender;
```

- `USING`을 사용한 쿼리와 `ON`을 사용한 두 쿼리는 같은 결과를 반환한다.
    - 하지만 `USING` 은 **두 테이블의 컬럼명이 같을 때** 이용할 수 있고,
    - `ON` 은 **두 테이블의 컬럼명이 다르더라도** `=` 비교를 통해 조인이 가능하다.



## 4. MySQL에서 인덱스(index)란 무엇인가요?

### 인덱스란
- 책의 목차와 같은 역할. 특정 데이터에 바로 접근할 수 있도록 데이터의 위치 정보를 제공해주는 기능이다.
- 모든 데이터베이스는 pk, fk에 자동으로 B+ Tree 인덱스를 생성한다.
- 인덱스가 있을 경우 O(log n)으로 탐색 가능
- index가 없는 컬럼은 O(n) 소요.
    - 인덱스가 걸리지 않은 컬럼으로 조회하면 전체 레코드를 풀스캔 하기 때문에 속도가 느리다.

### 인덱스 사용이유
- 검색성능 향상 목적 → 자주 사용하는 컬럼에 인덱스를 만들어 성능을 개선을 기대할 수 있다.
 - 해당 쿼리의 인덱스 사용 여부, 카디널리티, selectivity와 같은 요소들이 고려된 인덱스가 생성되어야 실제 성능 개선을 기대할 수 있다.

<br>
<hr>

### 참고
RDBMS과 NoSQL 비교
* https://codedragon.tistory.com/4195
* https://dataonair.or.kr/db-tech-reference/d-lounge/expert-column/?mod=document&uid=52606
* https://www.moreagile.net/2014/03/rdb.html
* https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=zx7024&logNo=60175836404
* https://owlyr.tistory.com/20
* https://broccoli45.tistory.com/46
* https://firststep-de.tistory.com/34
* https://sujl95.tistory.com/83


트랜잭션
* https://mangkyu.tistory.com/30](https://mangkyu.tistory.com/30
* https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=sophie_yeom&logNo=220245191398
* https://tecoble.techcourse.co.kr/post/2021-07-11-database-transaction/
* https://kosaf04pyh.tistory.com/202](https://kosaf04pyh.tistory.com/202
* https://joont92.github.io/db/트랜잭션-격리-수준-isolation-level/


JOIN
* https://www.w3schools.com/sql/sql_join.asp
* https://velog.io/@yanghl98/Database-JOIN
* https://doh-an.tistory.com/30
* https://seoyuun22.tistory.com/entry/SQL%EC%97%AC%EB%9F%AC-%ED%85%8C%EC%9D%B4%EB%B8%94%EC%9D%98-%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%A5%BC-%EC%A1%B0%EC%9D%B8%ED%95%B4%EC%84%9C-%EC%B6%9C%EB%A0%A5%ED%95%98%EA%B8%B0ON%EC%A0%88-USING%EC%A0%88-NATURAL-JOIN-LEFFTRIGHT-OUTER-JOIN
* https://linux.systemv.pe.kr/mysql-using-vs-%EC%B0%A8%EC%9D%B4/
* https://www.youtube.com/watch?v=dbkOk3JhxAE

인덱스
* https://itholic.github.io/database-cardinality/
* https://velog.io/@d3fau1t/%EC%9D%B8%EB%8D%B1%EC%8A%A4%EC%99%80-%EC%B9%B4%EB%94%94%EB%84%90%EB%A6%AC%ED%8B%B0
* https://www.youtube.com/watch?v=NkZ6r6z2pBg&t=702s
* https://jdm.kr/blog/169

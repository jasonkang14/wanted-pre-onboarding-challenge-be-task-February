1. 관계형 데이터베이스(RDBMS)와 비관계형 데이터베이스(NoSQL)의 장단점 비교

- 관게형 데이터베이스는 Relational database management system으로 관계형 모델을 기반으로 한 DBMS 유형입니다. 대표적으로 MySQL, SQL, ORACLE이 있다. NoSQL은 Not Only SQL로 MongoDB, Redis 등이 있습니다.
- RDBMS의 경우, 데이터 테이블 간의 관계가 있으며, JOIN이 가능합니다. 하지만 데이터 구조가 커지면서 복잡한 쿼리가 필요해질 수 있다는 단점이 있습니다. 그리고 스키마로 인해 데이터가 유연하지 못합니다.
- NoSQL은 자유로운 데이터구조를 가집니다. 하지만 데이터 간 관계성을 갖지 않아 데이터 중복이 발생하거나 수정에 따라 모든 데이터를 수정이 필요할 수 있다는 단점이 있습니다. RDBMS와 달리 Scale-up만이 아니라 Scale-out도 지원하기 때문에 성능 향상에 유리합니다.

2. 트랜잭션(transaction)이란 무엇인가요?

- 트랜잭션이란 데이터베이스 상태를 변화시키기 위핸 수행하는 작업의 단위입니다. 원자성, 일관성, 독립성, 지속성이라는 특성을 가지고 있습니다. 원자성은 트랜잭션이 모두 데이터베이스에 반영되거나 반영되지 않아야 한다는 것입니다. 일관성은 작업처리 결과가 일관되게 진행되는 것을 말하고, 독립성은 다른 트랜젝션에 영향을 주지 않는다는 것을 말합니다. 마지막으로 지속성은 트랜잭션의 결과가 영구적으로 반영됨을 의미합니다.
- 하나의 트랜잭션은 Commit되거나 Rollback 됩니다.
- 트랜잭션은 활동, 실패, 철회, 부분완료, 완료의 상태를 가집니다. 부분완료는 트랜잭션의 마지막 연산까지 실행되었으나, Commit 되기 전의 상태입니다.

3. MySQL에서 조인(join)의 역할은 무엇인가요? 다양한 join의 방식에 대해 설명해주세요.

- 조인이란 RDBMS에서 서로 다른 데이터 테이블의 연관된 자료를 가져오는 결합을 위해 사용되는 SQL 옵션입니다. 둘 이상의 테이블이 공통 컬럼으로 묶일 수 있다면 컬럼을 중심으로 두 테이블의 데이터를 불러올 수 있습니다.
```SQL
SELECT B.id, B.productName, B.amount, U.name, U.email, U.mobile
FROM Buy B
INNER JOIN User U
ON B.id = U.id
```
- JOIN은 여러가지 방식이 있는데 다음과 같습니다. 
  - INNER JOIN: 일반적으로 하나의 컬럼을 중심으로 양쪽 테이블의 결과 값이 있는 경우에는 두 테이블의 정보를 가져오기 위해 사용합니다.
  - (LEFT/RIGHT/FULL) OUTER JOIN: JOIN 컬럼을 중심으로 LEFT의 경우는 왼쪽 JOIN 테이블의 데이터를 모두 가지고 오고, RIGHT의 경우는 오른쪽 테이블의 모든 정보를 가지고 오는 방식입니다. FULL의 경우에는 모든 테이블의 정보가 누락없이 검색됩니다.
  - CROSS JOIN: 카티션 곱이라고도 하며, 한 쪽 테이블의 행별로 다른 테이블의 모든 행을 JOIN하는 방식입니다.
  - SELF JOIN: 자기 자신의 테이블에 조인하는 것으로 INNER JOIN, OUTER JOIN의 방식을 사용합니다.

4. MySQL에서 인덱스(index)란 무엇인가요?

- 인덱스란 추가적인 쓰기 작업과 저장 공간을 활용하여 데이터베이스 테이블의 검색 속도를 향상시키기 위한 자료구조입니다. INDEX를 활요하지 않으면 데이터베이스에서 조건절에 해당하는 내용을 찾기 위해 모든 데이터를 검색해야 합니다. 하지만 INDEX를 사용하면 조회속도와 성능을 향상 시킬 수 있습니다.
- 인덱스를 잘못 사용하면 오히려 성능이 안 좋아질 수 있음으로 사용하고자 하는 인덱스가 적합한지 잘 판단할 필요가 있습니다.


참조
* https://khj93.tistory.com/entry/Database-RDBMS%EC%99%80-NOSQL-%EC%B0%A8%EC%9D%B4%EC%A0%90
* https://mommoo.tistory.com/62
* https://coding-factory.tistory.com/226
* https://jaehoney.tistory.com/55
* https://mangkyu.tistory.com/96

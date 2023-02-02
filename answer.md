1. 관계형 데이터베이스(RDBMS)와 비관계형 데이터베이스(NoSQL)의 장단점 비교

- 관계형 데이터베이스는 고정된 행과 열로 구성된 테이블에 데이터를 저장합니다.
- 비관계형 데이터베이스는 표형식이 아니며, 관계형 테이블과는 다른 방식으로 데이터를 저장합니다. 주로 데이터가 고정되어 있지 않은 데이터베이스를 가리킵니다.

2. 트랜잭션(transaction)이란 무엇인가요?

- 트랜잭션이란 데이터베이스의 상태를 변환시키는 하나의 논리적 기능을 수행하기 위한 작업의 단위 또는 한꺼번에 수행되어야할 일련의 연산들을 의미합니다.
- 데이터베이스의 상태를 변화시킨다는 의미는 SQL질의어 SELECT, UPDATE, INSERT, DELETE를 이용하여 데이터베이스에 접근하는 것을 의미합니다.
- 작업단위는 사람이 정하는 기준에 따라 한꺼번에 모두 수행되어야 할 일련의 연산들을 뜻합니다.

3. MySQL에서 조인(join)의 역할은 무엇인가요? 다양한 join의 방식에 대해 설명해주세요.

- JOIN은 두 테이블을 결합하는 연산입니다.
- INNER JOIN, OUTER JOIN(LEFT JOIN, RIGHT JOIN), CROSS JOIN 이 있습니다.
- INNER JOIN, 두 테이블에서 같은 값만 가져옵니다.
- OUTER JOIN(LEFT JOIN), 왼쪽 테이블을 기준으로 오른쪽 데이블을 매치합니다.
- OUTER JOIN(RIGHT JOIN), 오른쪽 테이블을 기준으로 왼쪽 테이블을 매치합니다.
- CROSS JOIN, 조건에 부합하지 않는 행까지 포함시켜 결합하는 것입니다. 모든 경우의 수를 포함합니다.

4. MySQL에서 인덱스(index)란 무엇인가요?

- 인덱스는 저장된 데이터를 더 빠르게 찾을 수 있게 해주는 역할입니다.

<br/>
참고
<br/>
1.
<br/>
https://hanamon.kr/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-sql-vs-nosql/
<br/>
2.
<br/>
https://coding-factory.tistory.com/226
<br/>
https://cocoon1787.tistory.com/808
<br/>
3.
<br/>
https://dev-coco.tistory.com/59
<br/>
https://edudeveloper.tistory.com/69

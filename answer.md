# 프리온보딩 백엔드

1. 관계형 데이터베이스(RDBMS)와 비관계형 데이터베이스(NoSQL)의 장단점 비교
- RDBMS

관계를 맺고 있는 데이터가 자주 변경(수정)되는 어플리케이션이나 변결될 여지가 없고 명확한 스키마가 사용자와 데이터에 중요한 경우 사용한다.

특징 : 트랜젝션 지원이 강력하여 데이터가 안들어가는 경우는 있어도 잘못 들어가는 경우는 없다. 데이터 무결성을 보장한다

장점

1. 정해진 스키마에 따라 데이터를 저장해야 하므로 명확한 데이터 구조를 보장한다
2. 관계는 각 데이터를 중복없이 한 번만 저장할 수 있다
3. 복잡한 형태의 쿼리 가능

단점

1. 테이블 간 테이블 관계를 맺고 있어 시스템이 커질 경우 JOIN문이 많은 복잡한 쿼리가 만들어 질 수 있다
2. 성능 향상을 위해서는 서버의 성능을 향상 시켜야 하는 scale-up만을 지원한다. 이로 인해 비용이 기하급수적으로 늘어날 수 있다
3. 스키마로 인해 데이터가 유연하지 못하다. 나중에 스키마가 변경될 경우 번거롭고 어렵다

- NoSQL

데이터에 대한 캐시가 필요한 경우, 배열 형식의 데이터를 고속으로 처리할 필요가 있는 경우, 막대한 양의 데이터를 다뤄야하는 경우, 읽기 처리를 자주하지만 데이터를 자주 변경하지 않는 경우에 사용한다.

장점

1. 스키마가 없기 때문에 유연하며 자유로운 데이터 구조를 가질 수 있다. 언제든 저장된 데이터를 조정하고 새로운 필드를 추가할 수 있다
2. 데이터 모델 자체가 독립적으로 설계되어 있어 데이터 분산이 용이하며 성능 향상을 위한 scale-up 뿐만이 아닌 scale-out 또한 가능하다
3. 수평적 확장

단점

1. 데이터 중복이 발생할 수 있으며 중복된 데이터가 변경 될 경우 수정을 모든 컬렉션에서 수행해야 한다.
2. 스키마다 존재하지 않기에 명확한 데이터 구조를 보장하지 않으며 데이터 구조 결정이 어려울 수 있다.
1. 트랜잭션(transaction)이란 무엇인가요?
- 트랜잭션은 데이터베이스의 상태를 변화시키기 위한 작업 수행의 논리적 단위를 의미한다. 트랜잭션은 작업의 완전성을 보장한다. 작업 단위는 사용자가 특정 기능의 수행을 위해 SQL 작업을 묶은 단위를 의미한다. 트랜젝션은 ACID라는 4가지 특성을 만족해야한다
    - 원자성(Automicity)
    
    트랜잭션 내부에서 실행된 작업들은 모두 커밋되거나 모두 롤백되어야한다. 작업의 일부분만 성공할 수 없다.
    
    - 일관성(Consistency)
    
    모든 트랜잭션은 일관성있는 데이터베이스 상태를 유지해야한다. 시스템이 가지고 있는 고정요소는 트랜잭션 수행 전과 수행 완료 후의 상태가 같아야 한다.
    
    - 격리성,독립성(Isolation)
    
    둘 이상의 트랜젝션이 동시에 실행되고 있을 경우 어떤 하나의 트랜젝션이라도 다른 트랜잭션의 연산에 끼어들 수 없다. 수행중인 트랜잭션은 완전히 완료될 때까지 다른 트랜잭션에서 수행 결과를 참조할 수 없다
    
    - 지속성(Durability)
    
    트랜잭션이 성공적으로 완료되었을 경우,결과는 영구적으로 반영되어야한다.
    
1. MySQL에서 조인(join)의 역할은 무엇인가요? 다양한 join의 방식에 대해 설명해주세요.
- Join은 한 데이터베이스 내의 여러 테이블의 레코드를 조합하여 하나의 열로 표현한 것이다. 조인은 테이블로 저장되거나 그 자체로 이용할 수 있는 결과 셋을 만들어 낸다. join은 2개의 테이블에서 각각의 공통값을 이용함으로써 필드를 조합하는 수단이 된다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f0ddf29c-1905-4c73-a926-c7e5f8f144e6/Untitled.png)

1. INNER JOIN(내부 조인)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dc94cfff-043f-4fb9-bb76-91104ce51e0b/Untitled.png)

이너조인은 조인될 조건이 부합하는 행만을 가지고 온다. 교집합이 되는 각 테이블의 칼럼명을 ON이나 WHERE로 명시해준다

```
SELECT *  #해당되는 모든 컬럼을 가지고온다.
FROM 사원 # 사원테이블을 가져온다.
INNER JOIN 직책  # 사원테이블과 직책 테이블을 inner join한다.
ON 사원.직책번호 = 직책.직책번호; #사원테이블과 직책 테이블은 직책번호로 연결된다.

SELECT *  #해당되는 모든 컬럼을 가지고온다.
FROM 사원 # 사원테이블을 가져온다.
INNER JOIN 직책  # 사원테이블과 직책 테이블을 inner join한다.
WHERE사원.직책번호 = 직책.직책번호; #사원테이블과 직책 테이블은 직책번호로 연결된다.
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/adc6f451-98b2-4478-a5d6-07e76174d55c/Untitled.png)

이너조인은 두 테이블간의 교집합, 즉 겹치는 칼럼이 존재하는 경우에만 사용이 가능하다. 그렇지 않은 경우에는 아우터 조인을 사용한다.

1. OUTER JOIN(외부 조인)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8db74626-4b66-49f8-bfbc-941f134b127e/Untitled.png)

내부 조인은 두 테이블에 모두 데이터가 있어야만 결과가 나오지만, 외부 조인은 한쪽에만 데이터가 있어도 결과가 나온다. 아우터 조인은 두 테이블간의 교집합이 되는 데이터 뿐만 아니라 해당되지 않는 값 까지 가져온다. 처음으로 가져오는 기준이 되는 테이블(드라이빙 테이블)이 필요하다. OUTER JOIN은 LEFT OUTER JOIN, RIGHT OUTER JOIN, FULL OUTER JOIN 3가지가 존재하는데 LEFT와 RIGHT는 중간에 OUTER을 빼고 부르기도 한다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5c43bcdf-26bb-430a-910a-165ef4cf8761/Untitled.png)

- LEFT(OUTER) JOIN : 왼쪽 테이블의 모든 값 출력
    
    LEFT OUTER JOIN은 기준 테이블을 왼쪽에 두고 OUTER JOIN을 수행한다. 기준 테이블은 움직이거나 변형이 없고 대상이 되는 테이블이 변형된다. 
    
    ```
    SELECT *
    FROM A
    LEFT OUTER JOIN B
    ON A.학번 = B.학번
    ```
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a4b3f0ab-7808-4980-94e7-35bf36df0bc0/Untitled.png)
    
    이너 조인처럼 연결하면 초록색 부분이 추가되는데 10,21,99학번은 B테이블에 존재하지 않기 때문에 null로 체워진다
    
- RIGHT (OUTER) JOIN : 오른쪽 테이블의 모든 값 출력

RIGHT OUTER JOIN은 기준 테이블을 오른쪽에 두고 OUTER JOIN을 수행한다. 기준 테이블은 변형이 없고 대상이 되는 테이블이 변형된다.

```
SELECT *
FROM A
RIGHT OUTER JOIN B
ON A.학번 = B.학번
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/03805f2f-0524-4dd7-b214-e946f95e42ce/Untitled.png)

B테이블이 기준이므로 모두 가져온 후 학번으로 연결한다. A테이블에는 11,13,14학번이 없기 때문에 나이 성별 이름이 모두 null이 된다.

- FULL OUTER JOIN : 왼쪽 또는 오른쪽 테이블의 모든 값 출력

FULL OUTER JOIN은 왼쪽과 오른쪽 테이블의 모든 데이터를 읽어 결과를 생성한다. 즉, RIGHT JOIN + LEFT JOIN

```
SELECT *
FROM A
FULL OUTER JOIN B
ON A.학번 = B.학번
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/52dbe857-cc46-42e6-a260-3f64df72dfff/Untitled.png)

A 테이블과 B 테이블 모두 들어오고 그것에 따른 빈칸들까지 모두 null로 되어 표현된다.

- CROSS JOIN(상호 조인)

한쪽 테이블의 모든 행과 다른 쪽 테이블의 모든 행을 조인시키는 기능이다. 상호 조인 결과의 전체 행 개수는 두 테이블의 각 행 개수를 곱한 수만큼 된다. 카티션 곱이라고도 한다.

```
SELECT * FROM <첫번째 테이블>
CROSS JOIN <두번째 테이블>
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1d5a9322-5139-49ff-bf1a-69d447b47767/Untitled.png)

- SELF JOIN(자체 조인)

자체 조인은 자기 자신과 조인하므로 1개의 테이블을 사용한다. 별도의 문법이 있는 것은 아니고 1개로 조인하면 자체 조인이 된다.

```
SELECT <열 목록> FROM <테이블> 별칭 A
	INNER JOIN <테이블> 별칭B
	ON <조인될 조건>
[WHERE 검색 조건]
```

1. MySQL에서 인덱스(index)란 무엇인가요?
- 인덱스란 데이터의 저장(INSERT, UPDATE, DELETE)의 성능을 희생하고 그 대신 데이터 읽기 속도를 높이는 테이블의 동작속도(조회)를 높여주는 자료구조이다.  인덱스가 없더라도 데이터베이스를 작동하는데 있어서 문제 없지만 데이터베이스의 크기가 클수록 인덱스가 반드시 필요해진다. 인덱스는 데이터베이스의 성능(속도)를 크게 좌우하는 요소이기 때문이다.
    - select 검색 속도를 크게 향상 시킨다
    - 인덱스 생성 시 DB 크기의 약 10% 정도되는 추가 공간이 필요하다
    - 인덱스 생성 시 시간이 걸린다
    - insert, update, delete같은 데이터 변경 쿼리가 잦은 경우 페이징이 빈번해져 성능이 악화될 수 있다
    - 데이터 조회에는 플러스지만, 데이터 변경이 자주 일어나면 오히려 성능이 감소된다.
    
    인덱스의 타입은 크게 두가지로 나뉘는데 Primary(클러스터) 인덱스와 Secondary(보조) 인덱스로 나뉘어 진다. 클러스터 인덱스는 처음부터 정렬이 되어있는 영어 사전과 같은 개념이고, 보조 인덱스는 책 뒤의 찾아보기의 개념과 비슷하다. 각 인덱스의 특징에 따라 mysql에서 사용처가 다르다고 보면 된다.
    
    |  | 클러스터 인덱스 | 보조 인덱스 |
    | --- | --- | --- |
    | 속도 | 빠르다 | 느리다 |
    | 사용 메모리 | 적다 | 많다 |
    | 인덱스 | 인덱스가 주요 데이터 | 인덱스가 데이터의 사본(Copy) |
    | 개수 | 한 테이블에 한 개 | 한 테이블에 여러 개(최대 약 250개) |
    | 리프 노드 | 리프 노드 자체가 데이터 | 리프 노드는 데이터가 저장되는 위치 |
    | 저장값 | 데이터를 저장한 블록의 포인터 | 값과 데이터의 위치를 가리키는 포인터 |
    | 정렬 | 인덱스 순서와 물리적 순서가 일치 | 인덱스 순서와 물리적 순서가 불일치 |
    
    출처 : 
    [[MYSQL] 📚 인덱스(index) 핵심 설계 & 사용 문법 💯 총정리](https://inpa.tistory.com/entry/MYSQL-%F0%9F%93%9A-%EC%9D%B8%EB%8D%B1%EC%8A%A4index-%ED%95%B5%EC%8B%AC-%EC%84%A4%EA%B3%84-%EC%82%AC%EC%9A%A9-%EB%AC%B8%EB%B2%95-%F0%9F%92%AF-%EC%B4%9D%EC%A0%95%EB%A6%AC)

[SQL 기본 문법: JOIN(INNER, OUTER, CROSS, SELF JOIN)](https://hongong.hanbit.co.kr/sql-%EA%B8%B0%EB%B3%B8-%EB%AC%B8%EB%B2%95-joininner-outer-cross-self-join/)

[[2][SQL] JOIN 총 정리 - JOIN의 종류 및 설명(INNER JOIN, OUTER JOIN)](https://bramhyun.tistory.com/39)

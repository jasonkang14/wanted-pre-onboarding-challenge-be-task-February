1. 관계형 데이터베이스(RDBMS)와 비관계형 데이터베이스(NoSQL)의 장단점 비교

#### RDBMS (Relational Database Management Systems)
가장 널리 쓰이는 데이터베이스 형태로, 테이블 형태로 행, 열로 데이터를 구분하여 저장하는 형태이다.
여러 개의 테이블을 각자 목적에 맞게 만들고 그 테이블 사이에 중복되는 (공유되는) 자원을 기준으로
테이블 간의 관계를 설정하여 데이터베이스를 구성한다.

##### 장점
- ACID(Atomic, Consistent, Isolated, Durable) compliance
  - 안정적으로 트랜잭션이 일어날 수 있도록 해준다.
  - 트랜잭션 시에 데이터가 일부 변경되는 일이 일어나지 않도록 전체가 성공하거나, 실패하도록 한다.
- Data Accuracy
  - 정확한 데이터 정합성
  - Primary Key와 Foreign Key를 이용하여 중복되는 정보가 들어가지 않도록 할 수 있다.
  - 중복 데이터가 없으므로 데이터 정합성이 높아지게 된다.
- Normalization
  - 정규화
  - 정규화 과정을 통해서 비정상적인 데이터들을 줄이거나 제거할 수 있다.
  - 이렇게 데이터를 덜어냄으로써 보관 비용 절감 효과도 볼 수 있다.
- Simplicity
  - 간단함
  - 오래 전부터 가장 널리 쓰인 데이터베이스의 종류로, 리소스가 풍부하다.
  - 자연어와 비슷한 언어(SQL)로 되어있어서 비개발자도 쉽게 이해할 수 있다.
ㅎ
##### 단점
- Scalability
  - 확장성
  - RDMS는 역사적으로 1대의 머신에서 돌아가도록 설계되어있었다.
  - 즉, 하드웨어의 성능이 데이터 사이즈나 데이터의 양이 많아지면서 부족해지면, 하드웨어를 추가하는 식으로 성능 개선을 해야 한다는 단점이 있다. (Vertical Scaling)
- Flexibility
  - 유연함이 부족
  - 관계형 데이터베이스에서는 데이터 포맷과 길이를 미리 지정해놓아야 한다.
  - 데이터 간의 관계를 정의하기 위해서는 미리 지정하는 것이 더 편하겠지만, 데이터 구조를 바꿀 일이 생긴다면 굉장히 복잡해 질 것이다.
- Performance
  - 성능 문제(속도)
  - 촘촘하고 복잡하게 테이블 간의 관계가 얽혀있다 보니, 쿼리 수행 시간이 길어질 수밖에 없다.


#### NoSQL (Not-only SQL)
관계형 모형을 사용하지 않는 테이블 간의 조인 기능이 없는 데이터 베이스.
초고용량 데이터 처리, 단기간에 많은 수로 발생하는 데이터에 특화된 데이터 베이스로,
유연하고 높은 퍼포먼스를 내는 것이 특징이다.

NoSQL에서 사용되는 데이터 구조는 다음과 같다.

- Key-Value
  - 가장 기본적인 타입의 데이터베이스
  - 키-값으로 이루어진 페어의 형태로 저장된다.
  - Key는 데이터베이스에서 정보를 읽어올 때 사용된다.
  - 유니크한 Key 값을 가지고 저장되어 있기 때문에, 데이터를 읽고 쓰는 것이 매우 빠르다.
  - 하지만 너무 심플한 구조로 되어있어, 복잡다양한 Use case를 대응하는데는 부족하다는 것이 단점이다.

- Wide Column DB
  - 관계형 데이터베이스와 비슷하게 테이블, 행(row), 열(column)의 형태로 저장한다.
  - 하지만 각 행에 해당하는 열들이 모두 같은 이름과 포맷을 가질 필요는 없다.
  - 이 컬럼들은 심지어 복수의 서버에 걸쳐서 저장될 수도 있다.
  - Key-Value 데이터베이스처럼 유연하고, 쿼리 수행 속도가 빠르다는 장점이 있다.
  - 빅데이터를 다루는데 좋고, 구조화 되지 않는 데이터들을 다루는데 좋다.
  - 하지만 관계형 데이터베이스에 비해서 트랜잭션 속도가 현저히 느리다는 한계점이 있다.

![img_1.png](img_1.png)
- Document DB
  - 데이터를 문서 안에 저장한다.
  - 보통 JSON과 유사한 형태로 저장하게 된다.
  - 위의 예제에서는 Customer 1명의 데이터가 어떻게 저장되는지를 보여준다.
  - Customer 1명에 대한 모든 데이터를 한 곳에서 1장의 문서에 저장하고 있다.
  - 이 Document들은 JSON과 유사한 구조로 되어있기 때문에 가독성이 좋다.
  - 스키마가 없기 때문에 유연하고, 다양한 형태의 데이터들을 넣을 수 있기도 하다.
  - Non-relational 데이터베이스에서는 하드웨어를 확장해야 되는 것이 아니라(Vertical Scaling), 데이터베이스를 복수의 서버에 복제하여 Sync할 수 있는 형태로 확장이 가능하다.(Horizontal Scaling)


- Graph DB
  - 비관계형 데이터베이스 타입 중에 가장 특이한 데이터베이스이다.
  - 'Node'를 사용하여 데이터를 저장하고, 각 노드를 잇는 'Edge'로 관계를 정의한다
  - 그렇기 때문에 굉장히 속도가 빠르고, 새로운 노드와 엣지를 추가하는 것이 매우 쉽다.
  - 하지만 데이터베이스 전체를 아우르는 쿼리를 짤 때는 불편할 수밖에 없다. (관계가 정의되지 않은 곳도 있으므로)
  - 표준 쿼리 언어도 정의되지 않았고, 따라서 다른 graph 데이터베이스로 옮기려면 러닝커브가 상당하다.

Source: https://www.mongodb.com/compare/relational-vs-non-relational-databases      
Source: https://www.geeksforgeeks.org/difference-between-relational-database-and-nosql/

2. 트랜잭션(transaction)이란 무엇인가요?

#### Transaction
![img.png](img.png)
데이터베이스의 상태를 변환시키는 하나의 논리적 기능을 수행하기 위한 작업의 단위
또는 한꺼번에 수행되어야 하는 일련의 연산을 의미한다.

예를 들어, 웹사이트에서 사용자들이 한꺼번에 어떤 상품을 장바구니에 넣고 결제 버튼을 눌렀을 때,
재고 상태를 정확히 (더도 말고, 덜도 말고) 계산해야 하는데, 이럴 때 바로 데이터베이스의 트랜잭션이
사용된다.

다시 말해, 데이터베이스 트랜잭션은 '성공해서 업데이트했던가(Commit)' 아니면 '아예 일어나지 않은 상태로 되돌리는(Rollback)' 
둘 중의 하나의 상태만을 가진다.

```javascript
await session.withTransaction(async () => {
   const subtractMoneyResults = await accountsCollection.updateOne(
       { _id: account1 },
       { $inc: { balance: amount * -1 } },
       { session });
   if (subtractMoneyResults.modifiedCount !== 1) {
       await session.abortTransaction();
       return;
   }

   const addMoneyResults = await accountsCollection.updateOne(
       { _id: account2 },
       { $inc: { balance: amount } },
       { session });
   if (addMoneyResults.modifiedCount !== 1) {
       await session.abortTransaction();
       return;
   }
});
```

이 코드는 돈을 한 계좌에서 또 다른 계좌로 보내는 샘플 트랜잭션 코드이다. 
두 계좌 모두 반드시 성공해야만 업데이트 되고, 둘 중 하나라도 성공하지 못하면 해당 트랜잭션은 실패한다.

- Atomicity
  - 원자성
  - 모두 성공하거나 실패하는 케이스의 집합
  - 원자성을 보증함으로써 중간에 일부만 갱신되어 더 큰 문제가 생기는 것을 방지할 수 있다.
- Consistency
  - 일관성
  - 트랜잭션을 사용하는 가장 큰 장점 중 한 가지가 성공과 실패에 관계 없이 데이터 통합성을 유지할 수 있기 때문이다.
  - 트랜잭션은 데이터베이스 엔진이 승인한 방식으로만 데이터에 영향을 끼치기 때문에 항상 데이터가 일관되게 표시될 수 있도록 한다.
  - 예를 들어, 유저가 온라인 뱅킹 앱에 돈을 예치한다고 할 때, 즉시 반영된 값을 보고 싶어 한다. (즉시 반영되지 않는다면 유저는 자신의 돈이 없어졌다고 생각할 것이다.) 
- Isolation
  - 고립성
  - 모든 트랜잭션은 독립(고립)된 환경에서 실행되는 것을 보장해야 한다.
  - 그래야만 트랜잭션이 동시적으로 돌아갈 수 있다.
  - 예를 들어, 내 계좌에 돈이 $200있고, 각 $100씩 인출하는 2개의 트랜잭션이 동시에 시작되었다고 치자.
    - 트랜잭션은 각각 독립적이기 때문에 2개가 모두 완료되었을 때, 내 계좌에는 $100이 아닌 $0이 찍혀있을 것이다.
- Durability
  - 지속성
  - 지속성은 트랜잭션이 완료되고 상태가 업데이트 되었을 때, 그들이 영속적이라는 것을 보장한다.
  - 즉, 이 데이터들은 시스템이 다운되었거나 정전 등으로 꺼졌을 때도 계속 유지될 것이다.

Source: https://fauna.com/blog/database-transaction
Source: https://www.mongodb.com/basics/acid-transactions

3. MySQL에서 조인(join)의 역할은 무엇인가요? 다양한 join의 방식에 대해 설명해주세요. 

Join은 여러개의 테이블에서 공통적인 필드를 기반으로 테이블의 데이터를 검색하고 처리할 때 사용되는 명령절이다.

#### Inner Join / Cross Join
- Inner Join
  - 교집합의 형태로, 서로 겹쳐지는 부분의 데이터만 뽑아내는 것
- Cross Join
  - 보통 SQL에서에는 Inner Join과 다른점이 있지만, MySQL에서는 Inner Join과 똑같이 쓰인다. (대체 가능하다)
```sql
SELECT * FROM t1 LEFT JOIN (t2, t3, t4)
ON (t2.a = t1.a AND t3.b = t1.b AND t4.c = t1.c)
```
이 쿼리와
```sql
SELECT * FROM t1 LEFT JOIN (t2 CROSS JOIN t3 CROSS JOIN t4)
                 ON (t2.a = t1.a AND t3.b = t1.b AND t4.c = t1.c)
```
이 쿼리는 똑같은 쿼리라고 볼 수 있다.

#### Left Join / Right Join
- Left Join
  - Join 기준 왼쪽 테이블을 Outer Join(합집합)으로 가져오는 것
- Right Join
  - Join 기준 오른쪽 테이블을 Outer Join(합집합)으로 가져오는 것

#### Natural Join
- Inner Join의 일종으로 조인 조건 (ON 절)을 명시하지 않아도 됨
- 서로 이름이 같은 컬럼을 가져와서 조건으로 사용하는 형식
- 컬럼명이 변경되거나 할 때 모두를 확인해야 해서 유지보수성이 좋지 않음


Source: https://dev.mysql.com/doc/refman/8.0/en/join.html

4. MySQL에서 인덱스(index)란 무엇인가요?

#### Index

인덱스는 특정 컬럼의 값을 빠르게 가져올 수 있도록 사용되는 것이다. 인덱스가 없다면 MySQL은 맨 첫번째 행부터 하나씩 모든 테이블의 모든 행을 읽어나가야 할 것이다.
테이블이 거대할수록, 더 많은 비용이 드는 것이다. 만약 테이블이 인덱스를 가지고 있다면, MySQL은 빠르게 어디서 검색을 시작해야 할지 알 수 있을 것이다.

대부분의 MySQL 인덱스(Primary Key, Unique Key, FullText)는 B-tree로 되어있다. 

![img_2.png](img_2.png)

B-tree는 인덱스를 이루고 있는 자료구조의 한 종류로, 트리 구조를 이루고 있다.
B-tree는 Binary Search Tree와 비슷하지만 한 노드 당 자식 노드가 2개 이상 있을 수 있다.
검색 속도가 빠른 것이 큰 장점으로, Key 값과 트리 구조를 이용해 찾고자 하는 데이터를 찾는다.
B-tree 자체가 균형을 이루고 있으므로, 어떤 값을 찾더라도 같은 시간(O(logN))에 결과값을 얻을 수 있다.

MySQL에서는 하기 상황에 인덱스를 사용한다.
- WHERE절 조건과 일치하는 행을 찾을 때
- Join 절을 사용하여 테이블들에서 행을 반환할 때
- 특정 인덱스 컬럼에서 `min()`, `max()` 값을 찾을 때
- 테이블을 정렬하거나 그룹 지을 때

Hash Index는 MySQL의 Memory 보관 엔진에서만 쓰인다. (여기서도 B-tree 인덱스를 선택할 수 있다.)

##### B-tree와 Hash 인덱스 비교
- B-tree 인덱스
  - `=`, `>`, `>=`와 같은 부등호나 `BETWEEN` 같은 명령어로 컬럼을 비교할 때 사용될 수 있다. 
  - `LIKE` 비교에서 String의 첫 글자가 와일드카드(%)로 시작하지 않을 때도 사용될 수 있다.
  - `LIKE` 비교가 와일드카드로 시작하거나 3글자 이상 될 경우, MySQL은 Turbo Boyer-Moore 알고리즘으로 패턴을 초기화 하고, 이 패턴으로 빠르게 검색을 한다.
  - `AND`를 사용하여 여러개의 조건을 나열할 경우에는 모든 `AND` 그룹에서 인덱스가 있어야만 인덱스를 사용할 수 있다.

인덱스를 사용하는 경우
```sql
... WHERE index_part1=1 AND index_part2=2 AND other_column=3

    /* index = 1 OR index = 2 */
... WHERE index=1 OR A=10 AND index=2

    /* optimized like "index_part1='hello'" */
... WHERE index_part1='hello' AND index_part3=5

    /* Can use index on index1 but not on index2 or index3 */
... WHERE index1=1 AND index2=2 OR index1=3 AND index3=3;
```

인덱스를 사용하지 않는 경우
```sql
    /* index_part1 is not used */
... WHERE index_part2=1 AND index_part3=2

    /*  Index is not used in both parts of the WHERE clause  */
... WHERE index=1 OR A=10

    /* No index spans all rows  */
... WHERE index_part1=1 OR index_part2=10
```

- Hash 인덱스
  - `=` 혹은 `<=>`를 사용할 때만 사용된다. (하지만 굉장히 빠르다) 
  - 범위를 비교할 때는 사용되지 않는다(예: `>`)

Source: https://dev.mysql.com/doc/refman/8.0/en/mysql-indexes.html      
Source: https://dev.mysql.com/doc/refman/8.0/en/index-btree-hash.html
1. 관계형 데이터베이스(RDBMS)와 비관계형 데이터베이스(NoSQL)의 장단점 비교

- **관계형 데이터베이스(RDBMS, Relational DataBase Management System)** 는 `모든 데이터를 2차원 테이블 형태로 표현하는 데이터베이스로 다른 테이블과 관계를 맺고 모여있는 집합체`이다. 다른 테이블과의 관계를 나타내기 위해 외래키(foreign key)를 사용한다. 외래키를 이용해서 join이 가능하다는 것이 특징이다. 
  - 대표적으로 mysql, oracle, postgresql, mariadb 등이 있다.
  - **장점**
    - 정해진 스키마에 따라 데이터를 저장해야 하므로 명확한 데이터 구조를 보장한다.
    - 각 데이터를 중복없이 한번만 저장할 수 있다.
  - **단점**
    - 테이블 간의 관계를 맺고 있기 때문에 시스템이 커질 경우 join 문이 많은 복잡한 쿼리가 만들어질 수 있다.
    - 성능 향상을 위해서는 Scale-up만을 지원한다. 이로 인해 비용이 기하급수적으로 증가할 수 있다.
    - 스키마로 인해 데이터를 유연하게 관리할 수 없다. 나중에 스키마가 변경될 경우 번거롭다.   
    
  => 따라서, 데이터 구조가 명확하고 변경될 여지가 없는 명확한 스키마가 중요한 경우, RDBMS를 사용하는 것이 좋다.

<br>

- **비관계형 데이터베이스(NoSQL, Not Only Structured Query Language)** 는 RDBMS와 달리 **테이블의 관계를 정의하지 않는다.** RDBMS의 단점인 성능을 개선하기 위해 등장했다.
NoSQL은 key-value Database,Document Database, Wide Column Database, Graph Database와 같이 다양한 형태의 저장 기술을 지원하고 있다.  
    - 대표적으로 monodb, redis, dynamodb 등이 있다.
    - **장점**
      - 스키마가 없기 때문에 유연하고 자유롭게 데이터를 저장하고 관리할 수 있다.
      - 언제든지 저장된 데이터를 조정하고 새로운 필드를 추가할 수 있다.
      - 데이터 분산이 용이하며 성능 향상을 위한 Scale-up 뿐만 아니라 Scale-out도 가능하다.
    - **단점**
      - 데이터 중복이 발생할 수 있으며 중복된 데이터가 변경될 경우 수정을 모든 컬렉션에서 수행해야 한다.
      - 스키마가 존재하지 않기 때문에 명확한 데이터 구조를 보장하지 않으며 데이터 구조를 결정하기 어려울 수 있다.  

   => 따라서, 정확한 데이터 구조를 알 수 없고 데이터가 변경/확장될 수 있는 경우, 데이터 중복이 발생할 수 있는 경우이지만 Update가 많이 이루어지지 않는 경우(중복된 데이터가 변경될 시에는 모든 컬렉션에서 수정해야 하기 때문), 막대한 데이터를 저장해야 하는 경우(Scale-out이 가능하기 때문), NoSQL을 사용하는 것이 좋다.

<br>

2. 트랜잭션(transaction)이란 무엇인가요?

- **트랜잭션**이란, `데이터베이스의 상태를 변화시기 위해 수행하는 작업의 단위`를 뜻한다. 간단히 말해서 SELECT, INSERT, DELETE, UPDATE와 같이 질의어(SQL)를 이용하여 데이터베이스를 접근하는 것을 의미한다. 
이때 주의해야할 점은 작업의 단위는 질의어 한 문장이 아니라는 점이다. 작업단위는 사람이 정하는 기준에 따라 다양한 개수의 질의어 명령문이 될 수 있다.  
  - **특징**
    - **원자성(Atomicity)**: 트랜젝션이 데이터베이스에 모두 반영되거나 전혀 반영되지 않아야 한다.  
    - **일관성(Consistency)**: 단일 트랜잭션의 수행은 데이터 무결성을 유지한다. 트랜잭션 시작과 종료 시점에 무결성 제약을 만족해야 한다.  
    - **독립성(Isolation**): 다수의 트랜잭션이 동시에 수행되어도 사용자에게는 본인 트랜잭션이 홀로 수행되고 있는 느낌을 준다.
    - **지속성(Durability)**: 성공적으로 완료된 트랜잭션의 결과는 후에 시스템 장애가 발생할지라도 데이터베이스 상태에 반영되어야 한다.

<br>

3. MySQL에서 조인(join)의 역할은 무엇인가요? 다양한 join의 방식에 대해 설명해주세요.

- **조인**이란 `한 데이터베이스 내의 여러 테이블의 레코드를 조합하여 표현한 것`이다. 
조인은 테이블로서 저장되거나, 그 자체를 이용할 수 있는 결과 셋을 만들어 낸다. 
서로 관계있는 데이터가 여러 테이블로 나뉘어 저장되므로 각 테이블에 저장된 데이터를 효과적으로 검색하기 위해 조인이 필요하다.  
- **조인의 종류**
  - **내부조인(INNER JOIN)**
    `ex) SELECT * FROM employee INNER JOIN department ON employee.DepartmentID = department.DepartmentID`  
    - `inner`는 생략할 수 있는 키워드여서 join 연산은 내부 조인 연산을 의미한다.  
    - 내부 조인은 교집합과 동일하게 동작한다.
  - **외부 조인(OUTER JOIN)**
    - 외부 조인은 조인 연산에서 값 매치가 되지 않아 손실되는 정보를 유지하려고 하는 연산이다.  
    - 외부 조인 연산은 일차적으로 조인 연산을 수행하고, 조인 연산에서 제외된 터플을 널 값을 이용하여 결과 테이블에 첨가한다. 
    - 외부 조인에는 왼쪽 외부 조인(LEFT OUTER JOIN), 오른쪽 외부 조인(RIGHT OUTER JOIN), 완전 외부 조인(FULL OUTER JOIN)이 있다.
      - **왼쪽 외부 조인(LEFT OUTER JOIN)**
        `ex) SELECT * FROM emplyee LEFT OUTER JOIN department ON employee.DepartmentID = department.DepartmentID`  
        - 우측 테이블에 조인할 칼럼의 값이 없는 경우 사용한다.
        - 즉, 좌측 테이블의 모든 데이터를 포함하는 결과 집합을 생성한다.  
      - **오른쪽 외부 조인(RIGHT OUTER JOIN)**
        `ex) SELECT * FROM employee RIGHT OUTER JOIN department ON employee.DepartmentID = department.DepartmentID`  
        - 좌측 테이블에 조인할 컬럼의 값이 없는 경우 사용한다.
        - 즉, 우측 테이블의 모든 데이터를 포함하는 결과 집합을 생성한다.  
      - **완전 외부 조인(FULL OUTER JOIN)**
        `ex) SELECT * FROM employee FULL OUTER JOIN department ON employee.DepartmentID = department.DepartmentID`
        - 양쪽 테이블의 모든 데이터를 포함하는 결과 집합을 생성한다.  
  - **교차 조인(CROSS JOIN)**
    `ex) SELECT * FROM employee CROSS JOIN department`  
    - 교차 조인은 두 테이블 간의 가능한 모든 경우의 수에 대한 결과를 보여준다.
    - 즉, 카디널리티 곱을 한 것이다.  
  - **자연 조인(NATURAL JOIN)**
    `ex) SELECT * FROM employee NATURAL JOIN department`
    - 자연 조인은 두 테이블에서 동일한 이름을 가지는 속성 간에 조인 연산을 적용하며 결과 테이블에는 조인 속성에 대한 중복이 제거되어 한 번만 나온다.
    - 위의 예시 문장에서는 employee.DepartmentID와 Department.DepartmentID가 중복되는 속성이기 때문에, 자연 조인 결과로 중복 제거되어 한번만 나온다.
  - **동등 조인(EQUAL JOIN)**  
    `ex) SELECT * FROM employee, department WHERE employee.DepartmentID = department.DepartmentID`
    - 동등 비교 기반의 조인이며, 조인 구문에서 동등비교만을 사용한다.  
    - 다른 비교 연산자를 사용하는 것은 동등 조인으로서의 조인 자격을 박탈하는 것이다. 
  - **셀프 조인(SELF JOIN)**  
    `ex) SELECT * FROM employee e1 JOIN employee e2 ON e1.DepartmentID = e2.ExDepartmentID`
    - 다른 종류의 조인과는 다르게 다른 테이블을 참조하는 것이 아닌 자기 자신을 참조한다.  

<br>   

4. MySQL에서 인덱스(index)란 무엇인가요?

- **인덱스**란 `추가적인 쓰기 작업과 저장 공간을 활용하여 데이터베이스 테이블의 검색 속도를 향상시키기 위한 자료구조`이다. 
데이터베이스의 index는 데이터와 데이터의 위치가 포함된 자료구조를 생성하여 빠른 조회가 가능하도록 돕는 색인 역할을 한다.  
인덱스를 활용하면, 데이터를 조회하는 SELECT 외에도 UPDATE나 DELETE의 성능이 함께 향상된다. 그 이유는 해당 연산을 수행하려면 해당 대상을 조회해야만 작업을 할 수 있기 때문이다. 
- **인덱스의 관리**
  - DBMS는 index를 항상 최신의 정렬된 상태로 유지해야 원하는 값을 빠르게 탐색할 수 있다. 그렇기 때문에 인덱스가 적용된 컬럼에 INSERT, UPDATE, DELETE가 수행된다면 각각 다음과 같은 연산을 추가적으로 해주어야 하며 그에 따른 오버헤드가 발생한다.  
    - INSERT: 새로운 데이터에 대한 인덱스를 추가해야 한다.
    - DELETE: 삭제하는 데이터의 인덱스를 사용하지 않는다는 작업을 진행해야 한다.
    - UPDATE: 기존의 인덱스를 사용하지 않음 처리하고, 갱신된 데이터에 대해 인덱스를 추가해야 한다.
- **인덱스의 장점**
  - 테이블을 조회하는 속도와 그에 따른 성능을 향상시킬 수 있다.
  - 전반적인 시스템의 부하를 줄일 수 있다.
- **인덱스의 단점**
  - 인덱스를 관리하기 위해 DB의 약 10%에 해당하는 저장공간이 필요하다.
  - 인덱스를 관리하기 위해 추가 작업이 필요하다.
  - 인덱스를 잘못 사용할 경우 오히려 성능이 저하되는 역효과가 발생할 수 있다.
    만약 CREATE, DELETE, UPDATE가 빈번한 속성에 인덱스를 걸게 되면 인덱스의 크기가 비대해져서 성능이 오히려 저하되는 역효과가 발생할 수 있다. 그러한 이유 중 하나는 DELETE와 UPDATE 연산 때문이다. 앞에서 설명한대로, UPDATE와 DELETE는 기존의 인덱스를 삭제하지 않고 '사용하지 않음' 처리를 해준다고 하였다. 만약 어떤 테이블에 UPDATE와 DELETE가 빈번하게 발생된다면 실제 데이터는 10만건이지만 인덱스는 100만 건이 넘어가게 되어, SQL문 처리 시 비대해진 인덱스에 의해 오히려 성능이 떨어지게 될 것이다.


<br>
<br>

[참고자료]  
https://pythontoomuchinformation.tistory.com/528  
https://khj93.tistory.com/entry/Database-RDBMS%EC%99%80-NOSQL-%EC%B0%A8%EC%9D%B4%EC%A0%90   
https://mommoo.tistory.com/62  
https://velog.io/@ragnarok_code/DataBase-%EC%A1%B0%EC%9D%B8Join%EC%9D%B4%EB%9E%80  
https://hongcoding.tistory.com/146


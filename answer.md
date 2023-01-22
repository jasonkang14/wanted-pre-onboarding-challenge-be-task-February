1. 관계형 데이터베이스(RDBMS)와 비관계형 데이터베이스(NoSQL)의 장단점 비교

- `관계형 데이터 베이스`
    - 행과 열을 가지는 표 형식 데이터를 저장하는 형태의 데이터베이스를 가리키며, SQL 이라는 언어를 써서 조작합니다.
    - 종류에는 **SQL Server**, **Mysql**, **Oracle** 등이 있습니다.
- `비관계형 데이터 베이스`
    - SQL를 사용하지 않는 데이터베이스를 말합니다.
    - 종류에는 **MongoDB**와 **Redis** 가 존재합니다.
- `관계형 데이터 베이스`의 **장점**
    1. 스키마와 데이터에 대한 **무결성**을 보장합니다.
        
        **무결성이란 데이터의 정확성, 일관성, 유효성을 유지**하는 것을 말하며, 쉽게 데이터베이스에 저장된 데이터 값과 그 값에 해당하는 현실 세계의 실제 값이 일치하는지에 대한 신뢰를 줍니다.
        
    2. 관계는 각 데이터의 중복없이 한번만 저장시킬 수 있습니다.
- `관계형 데이터 베이스` 의 **단점**
    1. 데이터베이스안의 테이블간의 관계성이 유연하지 않습니다. ( 기능의 추가 등으로 수정이 필요한 경우 수정하기 어렵습니다 )
    2. 관계를 맺고 있기에 쿼리문이 복잡합니다.
    3. 대체로 수직적인 확장만 가능합니다.
        - 수직적인 확장이란 CPU나 RAM 같은 부품이나 하드웨어를 추가해주거나 교체를 하여 스케일업(Scale Up) 하는 경우를 말합니다.

2. 트랜잭션(transaction)이란 무엇인가요?
- 데이터베이스에서 하나의 논리적인 기능을 수행하기 위한 작업의 단위를 말합니다.  
이는 데이터베이스에 접근하는 방법은 쿼리이므로, 즉 여러 개의 쿼리들을 하나로 묶는 단위를 말한다고 볼 수 있습니다.
트랜잭션의 특징으로는 원일독지 → 원자성, 일관성, 독립성, 지속성 이 있습니다.

 
3. MySQL에서 조인(join)의 역할은 무엇인가요? 다양한 join의 방식에 대해 설명해주세요.

- 조인이란?
    - 하나의 테이블이 아닌 두 개 이상의 테이블을 묶어서 하나의 결과물을 만드는 것을 말합니다.
- 다양한 JOIN의 방식
    1. 내부 조인
        
        ![img1.daumcdn.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/16fd3f53-8041-4ac6-bb5d-628eb1ff8235/img1.daumcdn.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230122%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230122T080243Z&X-Amz-Expires=86400&X-Amz-Signature=9cb7786b129b47a9588b946eec0c6c7bc5df9bb2eaee0f9b1baa2aec29fed015&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22img1.daumcdn.png%22&x-id=GetObject)
        
        - 왼쪽 테이블과 오른쪽 테이블의 두 행이 모두 일치하는 행이 있는 부분만 표기합니다.
    2. 왼쪽 조인
        
        ![img1.daumcdn.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/35784f1c-7880-4e4c-8c6c-726ab7e979e8/img1.daumcdn.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230122%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230122T080338Z&X-Amz-Expires=86400&X-Amz-Signature=eb56bd3a1ff09a25e50a06bebec6c61b6fc457d04f7d3a4b3e20a65944bc8d64&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22img1.daumcdn.png%22&x-id=GetObject)
        
        - 왼쪽 테이블의 모든 행이 결과 테이블에 표시됩니다.
    3. 오른쪽 조인
        
        ![img1.daumcdn.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/51cc9ecb-ea2f-475f-a38d-b37afe5c5004/img1.daumcdn.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230122%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230122T080348Z&X-Amz-Expires=86400&X-Amz-Signature=22d72abb5dab392e7e16c45d662521e3d35bf822fe44cc04cf1c30620910df81&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22img1.daumcdn.png%22&x-id=GetObject)
        
        - 오른쪽 테이블의 모든 행이 결과 테이블에 표시됩니다.
    4. 합집합 조인
        
        ![img1.daumcdn.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8c68fff7-43ac-46c8-92a6-e59b73ea0798/img1.daumcdn.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230122%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230122T080400Z&X-Amz-Expires=86400&X-Amz-Signature=579e201915e217f577ce1b365fe3128b4cda5ec5611e2f05068a842526c1b457&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22img1.daumcdn.png%22&x-id=GetObject)
        
        - 두 개의 테이블을 기반으로 조인 조건에 만족하지 않는 행까지 모두 표기합니다.

4. MySQL에서 인덱스(index)란 무엇인가요?

- 인덱스란
    - 데이터를 빠르게 찾을 수 있는 하나의 장치입니다.
- 인덱스 동작 원리
    1. B-Tree
        - 인덱스는 B-Tree(Balanced Tree) 라는 자료 구조로 이루어져 있습니다.
        - 위 자료구조를 보면 이진트리 구조는 기존에 노드를 좌 우로밖에 뻗지 못하는 구조의 한계성이 있었습니다.
        하지만 B-Tree 자료구조는 노드를 2개 이상으로 뻗어나갈 수 있도록 만들어놓은 자료구조입니다.
        - 예시
            
            ![36f0703adadaf8cc9239.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7d2436dc-683d-4536-b632-8e80d24dfbcb/36f0703adadaf8cc9239.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230122%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230122T083022Z&X-Amz-Expires=86400&X-Amz-Signature=dc4c44fc7f41f502608f15a98472cd7a494142b730a96fa7d14b59725da76d50&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%2236f0703adadaf8cc9239.png%22&x-id=GetObject)
            
            - `35`를 찾는 다고 생각해봅시다.
            - 먼저 루트노드 20 40 를 탐색후 탐색하고자는 하는 `35` 값이 존재하지 않고, 20과 40 사이에 위치한다는 것을 인지합니다 이후 중간 노드로 탐색 수행
            - DEPTH 1 의 중간 노드를 왼쪽부터 탐색후 30 , 33 에 해당하는 값이 없고 33에 해당하는 값보다 탐색 값이 크다는 것을 인지합니다. 이후 오른쪽 노드로 이동
            - 35값을 찾았습니다!
            - 시간복잡도 ⇒ O(logn)
    2. 왜 B-Tree 자료구조를 도입하였나?
        - 효율적인 단계를 거쳐 모든 요소에 접근할 수 있는 균형 잡인 트리구조와 트리 깊이의 대수확장성에 유리하기에 도입하였습니다.
        
        > 대수 확장성
        트리 깊이가 리프 노드 수에 비해 매우 느리게 성장하는 것을 의미합니다.
        인덱스의 한 깊이가 증가시에 최대 인덱스 항목의 수는 4배씩 증가합니다.
        > 
        > 
        > ![download.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f45348bc-6baf-4ced-b6d4-bcca0dbf0934/download.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230122%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230122T083024Z&X-Amz-Expires=86400&X-Amz-Signature=939fbd6207162f210c958326bf333a1dbc80271dbeded0bc38adb66685191b8c&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22download.png%22&x-id=GetObject)
        >

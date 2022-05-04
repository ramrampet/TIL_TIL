### [Hacker Rank] Binary Tree Nodes
medium level [문제](https://www.hackerrank.com/challenges/binary-search-tree-1/problem?isFullScreen=true)

![image](https://user-images.githubusercontent.com/89775352/166670508-4e953879-4695-4bbe-b087-9de11833ba19.png)

-> 이걸 보면 CASE WHEN 문을 써야한다는 것을 알 수 있다. 

![image](https://user-images.githubusercontent.com/89775352/166671044-743c9a8b-9e78-4daa-aac1-4d17ec4aff95.png)

```sql
SELECT N,
    CASE WHEN N NOT IN (SELECT P FROM BST WHERE P IS NOT NULL) THEN 'Leaf'
         WHEN P IS NULL THEN 'Root'
    ELSE 'Inner' END
FROM BST
ORDER BY N

-- 의사 코드 작성 (노드 타입을 작성해라)
-- 1. N이 P에 포함되어있지 않으면 ->Leaf (부모가 아니다)
-- 2. P가 Null 이면 ->ROOT(부모가 없다)
-- 3. 둘다 아니면 ->INNER
-- 문제 : N이 P안에 포함되어있지 않으면에 NULL이 있다. 제거한 테이블: 서브 쿼리
```

되새기는 주의 사항 
- CASE 문 END 쓰는 거 까먹지 말기 
- CASE WHEN 으로 외워서 실수로 
```sql
CASE WHEN THEN 
CASE WHEN THEN 
```
이렇게 쓴다. CASE에 조건 여러개 일때는
```sql
CASE WHEN THEN 
     WHEN THEN 
     ELSE  END 
```
- Wrong Answer? : 쿼리문 제대로 다시 읽어보자 
- Write a query to find the node type of Binary Tree ordered by the value of the node. : ORDER BY N

- exists 랑 in 의 차이
- IN 에 칼럼이나 테이블을 가져올 수는 없지만 문자열이나 숫자를 기입하는 건 가능 
- 컬럼을 가져오려면 무조건 셀렉트, NULL이 있으면 계산이 안됨 exists 는 계산됨     

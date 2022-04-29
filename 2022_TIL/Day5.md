서브 쿼리 복습 
![image](https://user-images.githubusercontent.com/89775352/165936048-56dad068-b336-4fd4-a2d0-bc03dfe5da23.png)
이렇게 from절 서브쿼리로 묶으면 group by한 것을 하나의 테이블로 쓸 수가 있다.

leetcode 196. Delete Duplicate Emails

Write an SQL query to delete all the duplicate emails, keeping only one unique email with the smallest id. Note that you are supposed to write a DELETE statement and not a SELECT one.

Return the result table in any order.

```sql
DELETE FROM person
WHERE id NOT IN (
SELECT sub.min_id 
FROM (
SELECT email, MIN(id) AS min_id
FROM Person
GROUP BY email
)sub)
-- 어려우면 keeping 해야 하는 거 나누기!
-- WHERE 칼럼 기준으로 IN / NOT IN 
```



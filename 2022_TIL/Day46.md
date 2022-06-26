[607. Sales Person](https://leetcode.com/problems/sales-person/)
​
처음엔 간단하게 이렇게 풀면 된다고 생각했다.
​
```sql
SELECT s.name 
FROM  Orders o
      LEFT JOIN Company c ON c.com_id=o.com_id
      LEFT JOIN SalesPerson s ON s.sales_id=o.sales_id
WHERE c.name <> 'RED'
```
​
하지만.. 
​
Write an SQL query to report the names of all the salespersons who did not have any orders related to the company with the name **"RED"**.
​
Return the result table in **any order**.
​
The query result format is in the following example.
​
- 이건 다르다. 
​
- Not related니까 order 목록에 없는 sales person도 포함해야하고, 이런 로직들은 예시에서 파악하는 것이 좋다.
​
- (힌트를 주기 때문에!) 예시에서 힌트 알아차리기! 
​
```sql
SELECT name
FROM SalesPerson 
WHERE sales_id NOT IN (
                        SELECT o.sales_id
                        FROM  Orders o
                              JOIN Company c ON c.com_id=o.com_id
                        WHERE c.name= 'RED' 
                       )
```
​
[627. Swap Salary](https://leetcode.com/problems/swap-salary/)
​
```sql
UPDATE Salary SET sex=IF(sex='m','f','m')
```
​
UPDATE 에 IF 문을 써서 조건에 맞는 값으로 UPDATE 하고 싶을 경우 다음과 같이 사용하면 된다. 예시의 조건은 "TABLE 이라는 테이블에 C라는 컬럼의 값이 D 인것만 조회 후, A 컬럼을 C 컬럼 값이 D면 B
​
88240.tistory.com](https://88240.tistory.com/462)
​
[1084. Sales Analysis III](https://leetcode.com/problems/sales-analysis-iii/)
​
```sql
SELECT p.product_id
      ,p.product_name
FROM Sales s 
     JOIN Product p ON p.product_id=s.product_id 
WHERE p.product_id NOT IN (
                            SELECT product_id
                            FROM Sales s 
                            WHERE sale_date NOT BETWEEN '2019-01-01' and '2019-03-31'
                           )
```
​
[##_Image|kage@rzTfp/btrFGgCFJYn/AoN5ZAdUncbsSi8K969aT1/img.png|CDM|1.3|{"originWidth":1139,"originHeight":768,"style":"alignCenter"}_##]
​
- 역시 제외하여 쓰는게 정확! 
​
- Accepted 되었는데 제출하니 Wrong answer가 나왔다. 답도 맞는데..? 컴퓨터 문제인가 하여 discussion에 질문을 남겼다. Wish 🎁
​
내 질문 중 발췌 
​

> Select DISTINCT because you want one product to be returned just once, even if sales happened few times in requested period. And this solution of yours will return even products that are not even sold in requsted period, your only condition is that they are not sold outside the dates which is not enough. ;)
​
아 맞네.. 해당 예시에 집착하느라 결과론적으로 생각했다. 
​
그리고 id 하나만 뽑아주기를 원하니까 distinct! 
​
Discussion 활용하는 것 정말 좋다! 
​
바로 바꾼 내 쿼리
​
```sql
SELECT DISTINCT p.product_id
      ,p.product_name
FROM Sales s 
     JOIN Product p ON p.product_id=s.product_id 
WHERE s.product_id NOT IN (
                            SELECT product_id
                            FROM Sales s 
                            WHERE sale_date NOT BETWEEN '2019-01-01' and '2019-03-31'
                           )
```
​
#### **굿!** 
​
#### **배운점, 인사이트** 
​
-   역시.. 함정은 Example에서 조금이라도 힌트 준다, 그러니까 문제 대충 읽지 말기
-   리트코드는 지엽적인 문제인지, 괜찮은 문제인지 추천과 비추천 수로 가늠할 수 있다. 비추천이 과반 이상이면 지엽적인지 체크하고, skip할 수 있게 하기
-   UPDATE 함수에 아직 그렇게 익숙하지 않은데, IF 함수와 같이 쓰면 매우 유용하게 쓸 수 있을 것 같다! 
-   리트코드 무료로 공개되어있는 것 다시 다 풀고 유료 멤버십 결제 (한달 무료 :) )해서 마스터하기!   
-   흠.. discussion 잘 활용하기!

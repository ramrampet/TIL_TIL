[584. Find Customer Referee](https://leetcode.com/problems/find-customer-referee/)
​
```sql
SELECT name 
FROM Customer
WHERE referee_id <> 2 or referee_id IS null
```
-   그냥 WHERE referee\_id <> 2 해주니 NULL 값이 포함이 안되어서 이렇게 코드를 작성했다.
-   다른 분들은 어떻게 했나 Most votes를 클릭했더니 나와 같은 코드가 칭찬을 받고 있어서 뿌듯했다. 헷 

- 다른 풀이
이런 풀이도 있었다. 오... 
​
[586. Customer Placing the Largest Number of Orders](https://leetcode.com/problems/customer-placing-the-largest-number-of-orders/)
​
```sql
SELECT customer_number
FROM Orders
GROUP BY customer_number
ORDER BY COUNT(order_number) DESC 
LIMIT 1
```

-   집계 함수 중복해서 쓸 수 없다. MAX(COUNT(\*)) 이렇게는 못쓴다.
-   서브 쿼리등을 쓰려고 했는데 이 방법이 가장 효율적!

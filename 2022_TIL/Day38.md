## TIL
- solvesql 을 다수 다시 풀었다. 
```sql
WITH a AS (
SELECT r.customer_id
      ,r.order_id
      ,r.order_date
      ,DATE_FORMAT(r.order_date,'%Y-%m-01')as order_month
      ,DATE_FORMAT(c.first_order_date,'%Y-%m-01') as first_order_month
FROM records r 
    LEFT JOIN customer_stats c ON c.customer_id=r.customer_id
            )

SELECT first_order_month
      ,COUNT(DISTINCT customer_id) as month0
      ,COUNT(DISTINCT CASE WHEN DATE_ADD(first_order_month,INTERVAL 1 month)=order_month THEN customer_id END)month1
       ,COUNT(DISTINCT CASE WHEN DATE_ADD(first_order_month,INTERVAL 2 month)= order_month THEN customer_id END)month2
      ,COUNT(DISTINCT CASE WHEN DATE_ADD(first_order_month,INTERVAL 3 month)= order_month THEN customer_id END)month3
      ,COUNT(DISTINCT CASE WHEN DATE_ADD(first_order_month,INTERVAL 4 month)= order_month THEN customer_id END)month4
      ,COUNT(DISTINCT CASE WHEN DATE_ADD(first_order_month,INTERVAL 5 month)= order_month THEN customer_id END)month5
      ,COUNT(DISTINCT CASE WHEN DATE_ADD(first_order_month,INTERVAL 6 month)= order_month THEN customer_id END)month6
      ,COUNT(DISTINCT CASE WHEN DATE_ADD(first_order_month,INTERVAL 7 month)= order_month THEN customer_id END)month7
      ,COUNT(DISTINCT CASE WHEN DATE_ADD(first_order_month,INTERVAL 8 month)= order_month THEN customer_id END)month8
      ,COUNT(DISTINCT CASE WHEN DATE_ADD(first_order_month,INTERVAL 9 month)= order_month THEN customer_id END)month9
      ,COUNT(DISTINCT CASE WHEN DATE_ADD(first_order_month,INTERVAL 10 month)= order_month THEN customer_id END)month10
      ,COUNT(DISTINCT CASE WHEN DATE_ADD(first_order_month,INTERVAL 11 month)= order_month THEN customer_id END)month11
FROM a
GROUP BY first_order_month
ORDER BY first_order_month
```

```sql
SELECT order_date as dt 
     , COUNT(DISTINCT order_id) as dau
FROM records
WHERE order_date BETWEEN '2020-11-01' AND '2020-11-30'
GROUP BY dt
```

```sql
SELECT *
FROM tips
WHERE (size,total_bill) IN (
                            SELECT size
                                  ,MAX(total_bill)
                            FROM tips t 
                            GROUP BY size
                            )
ORDER BY size
```
- WHERE IN 절 서브쿼리 두개 컬럼, FROM 절 테이블 두개, 시간 정하기 등등
- 역시.. 늘 가던 곳! 

### 감사일기
- 나: 오늘 적당히 놀면서도 할 것을 한 나 자신에게 감사한다.
- 타인: 맛있는 식사 자리를 만들어준 레아와 친구들에게 감사하다.
- 물질: 마라탕에 푸짐한 토핑을 넣어서 먹을 수 있어서 감사하다.
- 경험: 스타벅스에서 커피와 케이크를 먹었는데 스트레스가 풀리는 기분이었다. 

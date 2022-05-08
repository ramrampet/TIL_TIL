- SQL로 리텐션을 구하고 COHORT 분석, 엑셀 시각화, 인사이트 도출하는 법을 배웠다.
- SQL로 group by한 날짜가 timestamp 라서 파이썬, 태블로로 시각화 하는 데에 불편함이 있었다. 추후에 보완하여 불편함을 없애야 겠다.
#### 각 월 별로 첫 구매한 고객이 몇 명인지 계산하기
```sql
SELECT l.first_order_month AS first_order_month
       ,COUNT(DISTINCT l.customer_id)month0
FROM(
     SELECT records.customer_id,records.order_id
     , DATE_FORMAT(records.order_date,'%Y-%m-01')order_month
     ,DATE_FORMAT(customer_stats.first_order_date,'%Y-%m-01')first_order_month
     FROM records
     INNER JOIN customer_stats ON records.customer_id= customer_stats.customer_id
     )l
GROUP BY first_order_month
```

#### 첫 결제한 달로부터 1~11개월 뒤에도 주문한 고객의 수
```sql
WITH pro AS(
SELECT r.customer_id
      ,r.order_id
      ,DATE_FORMAT(r.order_date,'%Y-%m-01')order_month
      ,DATE_FORMAT(c.first_order_date,'%Y-%m-01')first_order_month
FROM records AS r
INNER JOIN customer_stats AS c ON r.customer_id= c.customer_id
           )
SELECT first_order_month
      ,COUNT(DISTINCT customer_id)month0
      ,COUNT(DISTINCT CASE WHEN DATE_ADD(first_order_month,INTERVAL 1 month)= order_month THEN customer_id END)month1
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
FROM pro
GROUP BY first_order_month
ORDER BY first_order_month
```
#### 리텐션 백분율

```sql
WITH pro AS(
SELECT r.customer_id
      ,r.order_id
      ,DATE_FORMAT(r.order_date,'%Y-%m-01')order_month
      ,DATE_FORMAT(c.first_order_date,'%Y-%m-01')first_order_month
FROM records AS r
INNER JOIN customer_stats AS c ON r.customer_id= c.customer_id
           )
SELECT first_order_month
      ,concat(ROUND((month0/month0)*100,2),'%')month0
      ,concat(ROUND((month1/month0)*100,2),'%')month1
      ,concat(ROUND((month2/month0)*100,2),'%')month2
      ,concat(ROUND((month3/month0)*100,2),'%')month3
      ,concat(ROUND((month4/month0)*100,2),'%')month4
      ,concat(ROUND((month5/month0)*100,2),'%')month5
      ,concat(ROUND((month6/month0)*100,2),'%')month6
      ,concat(ROUND((month7/month0)*100,2),'%')month7
      ,concat(ROUND((month8/month0)*100,2),'%')month8
      ,concat(ROUND((month9/month0)*100,2),'%')month9
      ,concat(ROUND((month10/month0)*100,2),'%')month10
      ,concat(ROUND((month11/month0)*100,2),'%')month11
FROM(
SELECT first_order_month
      ,COUNT(DISTINCT customer_id)month0 
      ,COUNT(DISTINCT CASE WHEN DATE_ADD(first_order_month,INTERVAL 1 month)= order_month THEN customer_id END)month1
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
FROM pro
GROUP BY first_order_month
ORDER BY first_order_month
       )e
       ```

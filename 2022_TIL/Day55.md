### 레스토랑의 요일별 매출 요약
```sql
SELECT ROUND(AVG(l.sum_bill),2)
FROM (  SELECT SUM(total_bill) sum_bill 
        FROM tips
        GROUP BY day
      )l
```

#### 쇼핑몰의 일일 매출액

```sql
SELECT DATE(o.order_purchase_timestamp) as dt
      ,ROUND(SUM(pay.payment_value),2) as revenue_daily 
FROM olist_orders_dataset as o
     JOIN olist_order_payments_dataset as pay ON pay.order_id=o.order_id
GROUP BY dt
HAVING dt >= '2018-01-01'
ORDER BY dt
```
- ROUND 할 때 AS 실수하지 않기 
- TIMESTAMP, DATETIME 익히기 

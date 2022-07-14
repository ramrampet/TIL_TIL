## TIL 

#### 레스토랑의 요일별 매출 요약
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

#### 쇼핑몰의 일일 매출액과 ARPPU
- ARPPU는 Average Revenue Per Paying User의 약자로, 결제 고객 1인 당 평균 결제 금액을 의미합니다. 
- 전체 매출액을 결제 고객 수로 나누면 ARPPU를 계산할 수 있습니다.
```sql
SELECT DATE(o.order_purchase_timestamp)dt
      ,COUNT(DISTINCT customer_id)pu 
      ,ROUND(SUM(pay.payment_value),2)revenue_daily
      ,ROUND((ROUND(SUM(pay.payment_value),2)/COUNT(DISTINCT customer_id))
            ,2)arppu 
FROM olist_orders_dataset as o
     JOIN olist_order_payments_dataset as pay ON pay.order_id=o.order_id
GROUP BY dt
HAVING dt >= '2018-01-01'
ORDER BY dt
```

### 배운점, 인사이트
- 솔직히 쉽다고 느껴졌다. 이제 리트코드 프리미엄을 결제할 때가 온 것이다..
- 반복하면 느는게 실력!

## 감사일기
- 나: 매우 지쳤음에도 불구하고 카페에가서 늦게까지 할일을 하고 커밋을 한 나에게 감사하다.
- 타인: 나를 생각해서 물회를 포장해오신 아버지의 따뜻한 마음에 감사핟
- 물질: 서브웨이가 너무 맛있었다. 돈을 열심히 벌어야지
- 경험: 오랜만에 연락했는데 호인이가 많은 도움을 주었다. 은혜를 갚아야지. 


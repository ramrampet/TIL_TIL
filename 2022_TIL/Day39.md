## TIL
[**온라인 쇼핑몰의 Stickiness**](https://solvesql.com/problems/stickiness-of-shoppingmall/)

 DAU 구하기

```sql
SELECT order_date as dt 
     , COUNT(DISTINCT customer_id) as dau
FROM records
WHERE order_date BETWEEN '2020-11-01' AND '2020-11-30'
GROUP BY dt
```

WAU, Stickiness

```sql
WITH a AS(
SELECT order_date as dt 
     ,DATE_SUB(order_date, INTERVAL 6 DAY)days
     , COUNT(DISTINCT customer_id) as dau
FROM records
GROUP BY dt,days)

SELECT a.dt as dt 
      ,a.dau
      ,COUNT(DISTINCT customer_id) as wau
      ,ROUND( a.dau/COUNT(DISTINCT customer_id),2) as stickiness
FROM records r
     JOIN a ON r.order_date BETWEEN a.days AND a.dt
GROUP BY a.dt,a.dau
HAVING dt BETWEEN '2020-11-01' AND '2020-11-30'
ORDER BY dt
```

-   조인을 = 가 아닌 BETWEEN AND 로 연결하는 방식 이용 
-   BETWEEN a AND b 할때 a와 b 컬럼이 내가 비교하고자 하는 같은 테이블에 있는 것을 해야 함. orderdate는 이미 dt와 달라진 값! 
-   ROUND 안에 알리야스가 있으면 오류하 나지! 
-   WITH 절이 복잡한 쿼리 할때는 편하다. 

[월별 주문 리텐션 (롤링 리텐션)](https://solvesql.com/problems/monthly-rolling-retention/)

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
      ,COUNT(DISTINCT customer_id)month0
      ,COUNT(DISTINCT CASE WHEN DATE_ADD(first_order_month,INTERVAL 1 month)<= order_month THEN customer_id END)month1
      ,COUNT(DISTINCT CASE WHEN DATE_ADD(first_order_month, INTERVAL 2 month)<=order_month THEN customer_id END)month2
      ,COUNT(DISTINCT CASE WHEN DATE_ADD(first_order_month,INTERVAL 3 month)<= order_month THEN customer_id END)month3
      ,COUNT(DISTINCT CASE WHEN DATE_ADD(first_order_month,INTERVAL 4 month)<= order_month THEN customer_id END)month4
      ,COUNT(DISTINCT CASE WHEN DATE_ADD(first_order_month,INTERVAL 5 month)<= order_month THEN customer_id END)month5
      ,COUNT(DISTINCT CASE WHEN DATE_ADD(first_order_month,INTERVAL 6 month)<= order_month THEN customer_id END)month6
      ,COUNT(DISTINCT CASE WHEN DATE_ADD(first_order_month,INTERVAL 7 month)<= order_month THEN customer_id END)month7
      ,COUNT(DISTINCT CASE WHEN DATE_ADD(first_order_month,INTERVAL 8 month)<= order_month THEN customer_id END)month8
      ,COUNT(DISTINCT CASE WHEN DATE_ADD(first_order_month,INTERVAL 9 month)<= order_month THEN customer_id END)month9
      ,COUNT(DISTINCT CASE WHEN DATE_ADD(first_order_month,INTERVAL 10 month)<= order_month THEN customer_id END)month10
      ,COUNT(DISTINCT CASE WHEN DATE_ADD(first_order_month,INTERVAL 11 month)<= order_month THEN customer_id END)month11
FROM a      
GROUP BY first_order_month     
ORDER BY first_order_month
```

### 감사일기 
- 나: 오늘 wau 구하면서 어려웠는데 끝까지 포기하지 않고 과제를 다 푼 나자신 감사해!
- 타인: 비가 너무 왔어서 어머니가 데리러 와주셨다. 귀찮으셨을텐데 항상 감사하다. 잘해야지 
- 물질: 오늘 배민 쿠폰으로 어머니가 먹고 싶으시다는 짜장면과 탕수육을 시켰다. 어제 RJ 영상을 보고 내가 2022년 이 나이로 한국에서 살아가는 것은 정말 큰 천운이구나 생각했다.
- 경험: 오늘 면접 회고를 쓰면서 뭐랄까 경험이 더 충만해지는 걸 겪었다. 역시 회고!! 좋아 감사합니다

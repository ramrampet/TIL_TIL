- SQL 캠프 복습
```sql
# 테이블 피봇
SELECT day, ROUND(SUM(CASE WHEN time= 'Lunch' then total_bill ELSE NULL END),2) lunch
          , ROUND(SUM(CASE WHEN time= 'Dinner' then total_bill ELSE NULL END),2) dinner
FROM Tips
GROUP BY day

- 복습시 발견한 주의 점, Else NULL END 생략하지 말고 넣을 것 

# 첫 주문과 마지막 주문_solvesql 
안녕하세요 실전반 1주차 연습문제 <배송 예정일 예측 성공과 실패> 문제 질문 드립니다. 쿼리 오류가 나와서 
이전 질문들과 답변을 비교해보아도 어떤 것이 문제인지 찾지 못해 질문 드립니다.                                                                                                
SELECT DATE(order_purchase_timestamp)as purchase_date,
      COUNT(CASE WHEN order_delivered_customer_date <= order_estimated_delivery_date then order_id END)as success,
      COUNT(CASE WHEN order_delivered_customer_date > order_estimated_delivery_date then order_id END)as fail,
FROM olist_orders_dataset 
WHERE purchase_date BETWEEN '2017-01-01' AND '2017-01-31'
  AND order_delivered_customer_date IS NOT NULL
  AND order_estimated_delivery_date IS NOT NULL
GROUP BY purchase_date,success,fail
ORDER BY purchase_date
```
[다섯가지](https://assaeunji.github.io/etc/2021-10-24-tipsforjobs/)

[성장을 좋아하는 사람이, 성장하고 싶은 사람에게](https://www.slideshare.net/zzsza/ss-173453051)

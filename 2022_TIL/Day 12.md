데이터리안\_sql 캠프 연습 문제 질문 / 답변 복습 

Q 
solvesql 배송 예정일 예측 성공과 실패 문제 풀이 과정 복습

실전반 1주차 연습문제 <배송 예정일 예측 성공과 실패> 문제 질문 드립니다.

쿼리 오류가 나와서 이전 질문들과 답변을 비교해보아도 어떤 것이 문제인지 찾지 못해 질문 드립니다.

[solvesql 배송 예정일 예측 성공과 실패](https://solvesql.com/problems/estimated-delivery-date/)

```sql
SELECT DATE(order_purchase_timestamp)as purchase_date,
      COUNT(CASE WHEN order_delivered_customer_date <= 
           order_estimated_delivery_date then order_id END)as success,
      COUNT(CASE WHEN order_delivered_customer_date > 
           order_estimated_delivery_date then order_id END)as fail,
FROM olist_orders_dataset 
WHERE purchase_date BETWEEN '2017-01-01' AND '2017-01-31'
  AND order_delivered_customer_date IS NOT NULL
  AND order_estimated_delivery_date IS NOT NULL
GROUP BY purchase_date,success,fail
ORDER BY purchase_date
```

여기서 궁금한 것은

1\. 에러가 왜 나는지

2\. GROUP BY purchase\_date 만 적으신 분들이 많던데 success, fail 을 넣는게 맞는 것 아닌지 (빼도 에러가 났습니다)

3\. having절을 쓰지 않는 이유가 날짜를 지정해주고 카운트를 해서 인지 입니다.

A : (혜정님의 답변)

다람님, 세 가지를 수정해주시면 되는데요

1.  제이슨님이 말씀해주신 것 처럼 **WHERE 절에서는 SELECT 절에서 정의한 별칭을 사용할 수 없어요.** order\_purchase\_timestamp **컬럼 명을 그대로 사용해주셔야 하고, 이 컬럼은 시각까지 있는 컬럼이기 때문에 BETWEEN 조건을 걸 때 시각까지 포함해서 적어주시면 됩니다.**
2.  해당 **오류**가 나는 이유는 SELECT 절에서 정의하신 fail 컬럼 뒤에 **콤마(,)가 있어서 발생**합니다. 콤마를 삭제해주시면 해당 오류는 발생하지 않습니다.
3.  **GROUP BY 절에는 집계함수를 포함하지 않습니다**. **집계의 기준이 되는 컬럼만** 적어주면 되기 때문에 purchase\_date 컬럼만 적어주시면 됩니다.

별칭(alias) 사용 위치에 대해서는 아래 링크의 내용을 참고해주세요   
[https://www.mysqltutorial.org/mysql-alias/](https://www.mysqltutorial.org/mysql-alias/) 

**\-> 수정하여 통과한 코드** 

```sql
SELECT DATE(order_purchase_timestamp)as purchase_date,
      COUNT(CASE WHEN order_delivered_customer_date <= 
           order_estimated_delivery_date then order_id END)as success,
      COUNT(CASE WHEN order_delivered_customer_date > 
      order_estimated_delivery_date then order_id END)as fail
FROM olist_orders_dataset 
WHERE order_purchase_timestamp BETWEEN '2017-01-01 00:00:00' 
       AND '2017-01-31 23:59:59'
  AND order_delivered_customer_date IS NOT NULL
  AND order_estimated_delivery_date IS NOT NULL
GROUP BY purchase_date
ORDER BY purchase_date
```

**🚀 배운 것들 🚀**

**\- where 절에서는 select 절에서 정한 별칭을 사용할 수 없다.** 

(왜 그럴까? : 내 생각인데 원천 데이터에 일단 접근해야하기 때문에 이름표 나중에 단 거는

 group by 나 order by 에 쓰거나 서브쿼리로 쓸 때 가능할 거야)

**\- 그래서 Timestamp 데이터 그대로 써야하고, 시각 까지 명시해야해 '2017-01-01 00:00:00' 이런식으로**

(그리고 아까처럼 '2017-01-30 23:59:59' 이런식으로 써서 데이터 오류 나는 일 없도록 하자) 

\- **피봇 테이블 만들 때** 단어 몇개만 바꿔주면 되니까 복붙해서 적다보니 from 앞에 , 를 적어서 오류가 나는

  불상사 발생함. **from 절 앞에 , 붙어있나 확인하기**  

**\- Group by 절에는 집계함수 절을 포함하지 않음, 그래서 기준이 되는 컬럼만 적어주기가 가능**

**👀**

**\-** 열심히 돈벌어서 수강한 캠프니까 부족한 부분까지 뽕뽑자. 어려운 것 다시 복습하고 질문 슬랙 채널 적극 활용하자.

\- python / sql 문제 풀이 시 답 코드 구글링해서 어느정도 이해했다고 넘어가면 다시 마주했을 때 못푼다.

  -> 내 실력 아니다. 체화할 때 까지 분석해서 시간 걸리더라도 내것으로 만들기. 

\- solvesql 문제 만들어 주신게 실제 sql 코딩 테스트 문제와 유사하다. 적극 활용하기

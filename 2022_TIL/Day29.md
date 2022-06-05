![image](https://user-images.githubusercontent.com/89775352/172053234-f45d9156-3edc-4f3e-b5b9-dce5ecbda111.png)

20220605
나 다른 사람 물질 경험 
1. 나는 오늘 노션 할일을 다해서 기특하다 
2. Leah가 우리가 만나서 너무 기쁘다고 fate 같다고 했다. 레아는 정말 착한것 같다. 레아와 같은 선생님을 만나서 감사하다.
3. Leah에게 팔찌를 사줬는데 돈이 아깝지 않을 정도의 돈을 가지고 있음에 감사합니다.
4. 오늘 면접왕 이형의 강의가 너무 좋아서 바로 적용할 수 있었고 그로스 해킹 책의 적용점을 블로그에 적을 수 있어서 그런 경험에 감사합니다. 

﻿레스토랑 웨이터의 팁 분석 

복습 중.. 쉬운 문제라고 방심하고 문제를 제대로 읽지 않은 것이 화근이었다.

평균 팁과 평균 일행 수는 소수점 아래 셋째 자리에서 반올림 해 둘째 자리까지 출력하고

를 대충 보고 셋째 자리 까지 ? 오케이 ROUND( , 3) 을 해주었다. 결과는? 당연히 오류! 

셋째 자리에서~ 둘째 자리 까지!! 실력이 조금 늘었다고 문제를 제대로 안보는 그런 자만 좋지 않아요 :)

반성하는 계기가 되었다.

```sql 
SELECT day
     , time
     , ROUND(AVG(tip),2) AS avg_tip
     , ROUND(AVG(size),2) AS avg_size
FROM tips t 
GROUP BY day, time 
ORDER BY day, time
```

할부는 몇 개월로 해드릴까요


와.. 역시 이런 함정을 일부러 의도하신 것이 었어.. 쉬운데..? 왜 정답률이 17%지 했다...



1. 처음 풀이 

```sql 
SELECT payment_installments 
     , COUNT(order_id) AS order_count
     , MIN(payment_value) as min_value
     , MAX(payment_value) as max_value
     , AVG(payment_value) as avg_value 
FROM olist_order_payments_dataset
GROUP BY payment_installments
```

-> 오답 채점이 나왔다. 왜지? 하고 자세히 문제를 더 봤는데...



" 신용카드로 주문한 내역을 할부 개월 수 별로"


조건을 하나 더 넣었어야 했어..! 역시..

문제 받았을 때 처음에 데이터 용량 초과 걸리는거 limt으로 걸고 전체 데이터의 shape을 검토해볼 필요가 있는 게 

이러한 문제 파악의 용이성 때문에..! 

```sql 
SELECT * 
FROM olist_order_payments_dataset
LIMIT 100
```

이런식으로 확인해 봐야지 어떤 조건을 넣어줘야할지 알 수 있다!

```sql 
SELECT payment_installments 
     , COUNT(order_id) AS order_count
     , MIN(payment_value) as min_value
     , MAX(payment_value) as max_value
     , AVG(payment_value) as avg_value 
FROM olist_order_payments_dataset
WHERE payment_type='credit_card'
GROUP BY payment_installments
```
이제..되겠지? 


???? 내내 걸렸던 payment sequential 문제인가봐.. 

2행, order_count 컬럼의 값이 일치하지 않습니다. (쿼리 결과: 25455, 정답: 25407)

--> 48개의 order_count가 줄어야 한다. 



그런데  payment sequential 연속 결제수를 어떻게 처리해줘야할지에 대한 도메인 지식이 부족했다. 

그래서 일단 연속 결제를 단건으로 처리해줘야하면 연속 결제 피쳐가 2부터인 것을 뽑아보자고 생각했다.
```sql 
SELECT *
FROM olist_order_payments_dataset
ORDER BY order_id
WHERE payment_sequential >1 
LIMIT 200
```
하지만 이렇게해서 보았을 때는 명확한 방법이 떠오르지 않았다. 

그냥 EDA를 하다보니 비록 카드는 아니지만 이런 결과가 보여 Distinct를 써주자 라는 생각이 들었다. 

```sql 
SELECT payment_installments 
     , COUNT(Distinct order_id) AS order_count
     , MIN(payment_value) as min_value
     , MAX(payment_value) as max_value
     , AVG(payment_value) as avg_value 
FROM olist_order_payments_dataset
WHERE payment_type='credit_card'
GROUP BY payment_installments
```
하... ✌ 물론 주관적 경험이지만 요새 꾸준히 괄호안에 DISTINCT 를 넣어주면 풀리는 경험들을 많이 하고 있다.

따라서

에러가 나면? (결과 값이 정답보다 많을 때)
1. 빠뜨린 조건이 없나 살펴보고
2. DISTINCT를 써야하지는 않나 생각해보기!

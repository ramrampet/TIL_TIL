## TIL
[1050. Actors and Directors Who Cooperated At Least Three Times](https://leetcode.com/problems/actors-and-directors-who-cooperated-at-least-three-times/)

```
SELECT actor_id, director_id
FROM ActorDirector 
GROUP BY actor_id, director_id
HAVING COUNT(*)>=3
```

성능, 문제 풀이 속도 만족 문제 자체는 쉬웠다.

#### **배운점 인사인트** 

-   대신  discussion에 most votes가 나와 같은 풀이였는데 having count(1)>=3 이렇게 썼다. 이것의 의미는  첫번째 칼럼의  갯수를 count하는 것과 동일하다는 것을 배웠다. 

[1158. Market Analysis I](https://leetcode.com/problems/market-analysis-i/)

```
SELECT IFNULL(Column명, "Null일 경우 대체 값") FROM 테이블명;
```

```
SELECT u.user_id as buyer_id
      ,u.join_date
      ,IFNULL(COUNT(order_date),0) as orders_in_2019
FROM Users u  
     LEFT JOIN Orders o ON o.buyer_id=u.user_id AND YEAR(o.order_date)='2019'
GROUP BY u.user_id
```

Success

[Details](https://leetcode.com/submissions/detail/751062223/) 

Runtime: 980 ms, faster than 89.01% of MySQL online submissions for Market Analysis I.

Memory Usage: 0B, less than 100.00% of MySQL online submissions for Market Analysis I.

#### **배운점 인사인트** 

-   0 카운트를 포함해야함으로 , output의 형태를 고려했을 때 orders table이 아닌 users에 left join하는게 맞다.
-   또한 if null을 할 때 count(distinct order\_id)를 해주어서 자꾸 오답이 나왔는데, left join을 YEAR(o.order\_date)='2019' 조건으로 걸어주었음으로 order\_date가 null일때 0으로 지정해줘야하기 때문에 count(order\_date) 가 맞다.
-   또한 o. buyer\_id로 그룹바이 했을 때 오답이 나왔는데 아무래도 조인을 왼쪽을 기준으로 해주었기 때문에 그런 것 같다. 이 부분에 대해서 질문하는 사람도 있었는데  더 알아봐야겠다.

#### **피시방 코딩 소감** 

-   한참 본가에 있다가 집 보러 올라와서 노트북을 챙기는 것을 깜빡했다. 노트북을 못하다니.... 손이 근질근질하고 심심하여 리트코드라도 몇문제 풀자 싶어 피시방에 왔다. 약간 스스로에게 은은한 현타감과 모두가 게임을 하는 이 상황에 나혼자 코딩을 하자니 코딩이나 게임이나 비슷한 경계에 놓였다는 생각이 들었다. 진한 담배 연기, 욕설과 함께 하는 문제 풀이란...나에게 롤? 과 같은 놀이로 더욱 정착하도록 재미를 더 붙여야겠다.
-   역시 안하면 서운하고 허전한 너란 존재.. 고마워

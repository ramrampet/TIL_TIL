### 오늘 감사할 거리 
- 나: 나는 자신감을 잃지않고 1시~12시까지 열심히 쭉 공부하였다. 그런 열정 넘치는 나 감사해! 
- 다른 사람: 레아가 오늘 같이 공부해주러 왔다. 할머니가 용돈 10만원을 주시면서 사랑해주셨다. 감사합니다!
- 물질: 오늘 10만원이 생겼다! 
- 경험: 호인이와 같이 줌으로 공부할 수 있어서 행복하다 :) 

### TIL 
![image](https://user-images.githubusercontent.com/89775352/172189304-f8f68269-5320-43fe-b3b1-824b9aa0f841.png)

- 그로스 해킹 책에서 많이 배웠다! 이 부분을 레퍼런스 삼아서 면접 준비와 미래의 하고 싶은 것들을 많이 적어야 겠다. 

Solvesql [데이터 그룹으로 묶기](https://solvesql.com/problems/group-by/)

-  평균, 표본 분산 등을 그룹핑하여 푸는 문제
​
헷갈릴 수 있는 포인트 

- DBMS에 따라 표본 분산을 구하는 함수가 다를 수 있다
​
- VARIANCE() 를 취하면 표본 분산이 아닌 모분산을 구하게 된다. 이 부분 때문에 처음에 헷갈렸다. 
​
이 부분은 통계학적 지식이 조금 가미되어야 하는데, 다시 헷갈리지 않도록 정리해보도록 하겠다. 
​
reference : [w3resource](https://www.w3resource.com/mysql/aggregate-functions-and-grouping/aggregate-functions-and-grouping-var_pop().php)
​
VAR\_SAMP() : the sample variance (표본 분산) 
​
VARIANCE() : the population standard variance (모분산)

![image](https://user-images.githubusercontent.com/89775352/172187831-6518fb70-b828-40eb-bf5d-1d51f3cdc1d1.png)


정답 코드 
​
```sql
SELECT quartet
    , ROUND(AVG(x),2) AS x_mean
    , ROUND(VAR_SAMP(x),2) AS x_var
    , ROUND(AVG(y),2) AS y_mean
    , ROUND(VAR_SAMP(y),2) AS y_var
from points 
GROUP BY quartet
```
​
그런데 여기서 사실 문제가 있었다. 

![image](https://user-images.githubusercontent.com/89775352/172187792-e3192723-4d31-4715-b0b5-b29dd9d73c44.png)

라고 되어있어서 당연히 처음에 ROUND(,1)을 해주었는데 제출 결과
​
소수점 둘째자리까지의 출력을 원하여 틀린 답이 되었다. 
​
- 그래서 (???) 내가 잘못 알고 있는게 있나? 하며 '소수점 아래 둘째자리 반올림', '소수점 아래' 를 구글링 하며 열심히 초등학생과 중학생의 공부 풀이를 다시 마주했다... ㅎㅎ 문   제 오류인것 같아 결론적으로 슬랙에 질문을 남겼고 

- 문제가 오류가 있는 것 같다고 짚어주셔서 ??? 가 풀리게 되었다. 이 문제는 '쉬움' 난이도임에도 불구하고 정답률이 22%였는데 많은 분들이 문제 오류겠거니 하고 넘어가신것 같다.

[Leetcode_180. Consecutive Numbers](https://leetcode.com/problems/consecutive-numbers/)
```sql
SELECT a.num as ConsecutiveNums 
FROM   (
        SELECT id
              ,num
              ,(LEAD(num,1) OVER (ORDER BY id))l
              ,(LEAD(num,2) OVER (ORDER BY id))m
        FROM logs
        )a
WHERE a.num=a.l AND a.num=a.m AND a.l=a.m   
```
![image](https://user-images.githubusercontent.com/89775352/172189953-9d6a2724-e9e7-4be1-8848-3b26a421f74c.png)


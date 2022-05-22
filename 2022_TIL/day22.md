[HackerRank_symmetric-pairs](https://www.hackerrank.com/challenges/symmetric-pairs/problem?isFullScreen=true) 


1\. 여기서 f2.X, f2.Y를 없애주면 자꾸만 오답이 나왔다. 

   중복값이 문제인가 해서 SELECT DISTINCT 해줘도 그대로였다. 

   그래서 뭐가 문제인지 고민해봤다. 

```sql
SELECT f.X
      ,f.Y
      ,f2.X
      ,f2.Y
FROM Functions f
     JOIN Functions f2 ON f.X=f2.Y
WHERE f2.X=f.Y AND f.Y >= f.X
ORDER BY f.X
```

2\. 여기서 결과값을 봐도 알 수 있듯이 (5,5)와 같은 것은 설명대로 symmetric pairs가 아니라 값이 하나라도 조건을 통과하게 된다. 이런 점을 위해 sample input을 보면 힌트를 주는 것을 알 수 있다. 20,20 은 2쌍이 있어야지 답으로 인정된다. 그래서 distinct를 준 것은 당연히.. ㅎㅎㅎ 

\- 이제는 (2,2) 와 같은 값은 두개가 있어야 한다는 조건을 하나 더 걸어주도록 하겠다.

\- 그럼 어떻게 해야할까 group by를 써야겠지요 

\- X=Y면 이 값이 한개 초과여야하고, 아니면 X<Y여야 한다는 조건을 추가로 걸어 주도록 하겠다.

```sql
SELECT f.X AS X1
      ,f.Y AS Y1
FROM Functions f
     JOIN Functions f2 ON f.X=f2.Y
WHERE f2.X=f.Y 
GROUP BY X1,Y1
HAVING COUNT(*)>1 OR X1<Y1
ORDER BY f.X
```

https://solvesql.com/problems/multiple-medalist/

solvesql.com


복수 국적자 찾으려면? 조금씩 풀이를 해보려고 

이렇게 했다. 
```sql
SELECT r.athlete_id as aid
      ,COUNT(*)
FROM records as r 
WHERE medal IN ('Silver','Gold','Bronze')
GROUP BY aid 
LIMIT 100
```
하지만 역시 여러개가 조인 가능한 테이블이 있으면 그곳에 다중 조인을 하는 것이 더 효과적이다, 

그리고 그냥 JOIN 을 해버리면 다 붙어있는 records의 많은 부분이 생략되어 나타남으로 LEFT JOIN을 하는 것이 맞다. 



- 그리고 공백과 null은 달라서 is not null로 해줬는데 여기서는 왜 이게 되는걸까? 

: mysql에서 공백과 null은 같은 것? 질문함 

```sql
SELECT a.name
FROM records r 
    LEFT JOIN athletes a ON a.id=r.athlete_id
    LEFT JOIN teams t ON t.id=r.team_id
    LEFT JOIN games g ON g.id=r.game_id 
WHERE g.year >=2000 AND r.medal IS NOT NULL
GROUP BY athlete_id
HAVING COUNT(distinct team) > 1
```

- 계속 어떻게 국적이 두개인 것을 알아낼까, 셀프 조인해야하나 생각해야하는데 간편한 distinct를 잊었다니..! 


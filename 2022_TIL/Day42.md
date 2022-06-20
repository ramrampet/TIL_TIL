## TIL
[176.Second Highest Salary](https://leetcode.com/problems/second-highest-salary/)

```
SELECT MAX(salary) AS SecondHighestSalary 
FROM Employee
WHERE salary < (SELECT MAX(salary) FROM Employee)
```

\- 테스트 케이스를 맞추기 위한 풀이 

[178. Rank Scores](https://leetcode.com/problems/rank-scores/)

```
SELECT score, DENSE_RANK() OVER (ORDER BY score DESC)rank 
FROM Scores 
ORDER BY rank
```

[1050\. Actors and Directors Who Cooperated At Least Three Times](https://leetcode.com/problems/actors-and-directors-who-cooperated-at-least-three-times)

```
SELECT actor_id,director_id
FROM ActorDirector
GROUP BY actor_id,director_id 
HAVING COUNT(*)>=3
```

1068. Product Sales Analysis I

```
SELECT p.product_name
      ,s.year
      ,s.price
FROM Sales s
    JOIN Product p ON p.product_id=s.product_id
```

1069. Product Sales Analysis II

```
SELECT p.product_id
      ,SUM(s.quantity) as total_quantity
FROM Sales s
    JOIN Product p ON p.product_id=s.product_id
GROUP BY p.product_id
```

## 감사일기
- 나: 오늘 푹 잔 나에게 감사하다
- 타인: 동네 친구가 생겨서 감사하다!!
- 물질: 쌍화탕을 2개나 매일 플렉스할 수 있는 여유라니...
- 경험: 고민을 함께 같은 분야에 관해 털어놓을 수 있는 분들이 계셔서 감사하다. 전문적인 분야에 종사하시는 분들이 나와 같은 사람들을 도와 주려고 하신다는 것, 그리고 그런 
- 플랫폼에 감사드린다. 

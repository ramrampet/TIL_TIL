[HackerRank Ollivander's Inventory](https://www.hackerrank.com/challenges/harry-potter-and-wands/problem?isFullScreen=true)

왜 이렇게하면 안될까? 
```sql
SELECT w.id,p.age,w.power,MIN(w.coins_needed)
FROM Wands AS w
JOIN Wands_Property AS p ON w.code=p.code
WHERE p.is_evil=0
GROUP BY w.id,p.age,w.power
ORDER BY w.power,p.age DESC
```
--> 이렇게 하면 w.id 값이 고유하기 때문에 각자 각 하나의 값의 최솟값을 구하게 된다. = 자기자신 

그렇기 때문에 서브쿼리를 통해서 최솟값을 구해줘야하는 거다! 



이 풀이에는 다양한 방법이 있는데

1. Where절 서브쿼리 방법

2. From절 서브쿼리 방법이 있다.



하지만 기본 논리는 같음으로 Where절 서브쿼리 방식으로 풀어보겠다.  



조건 

-- power와 age가 같을 때 최소의 코인을 지불한다.



-> 그러면 power와 age를 GROUP BY 해주고 거기에 맞는 최솟값을 출력해줘야한다.

    그런데 우리가 고유한 값 id를 출력해줘야하니까 셀프조인을 통해 서브쿼리를 만들어야하는 것  

-- evil=0이어야 한다
-- desc power, desc age


```sql
--내 풀이

SELECT w.id,wp.age, w.coins_needed,w.power
FROM Wands w 
JOIN Wands_Property wp ON w.code=wp.code
WHERE w.coins_needed= (SELECT MIN(coins_needed) FROM Wands w2
                       JOIN Wands_Property wp2 ON wp2.code=w2.code
                       WHERE wp2.is_evil=0 AND wp2.age=wp.age 
                       AND w.power=w2.power)
ORDER BY power DESC, age DESC

--ㅎㅇ 님 풀이

select id
        ,age
        ,coins_needed
        ,power
from wands w1
join wands_property p1 on w1.code = p1.code
where w1.coins_needed = (select MIN(coins_needed)
    from wands w2
    join wands_property p2 on w2.code = p2.code
    where is_evil = 0
    and p2.age = p1.age and w1.power = w2.power)
order by w1.power desc, p1.age desc
```
여기서 p2.age = p1.age and w1.power = w2.power 이렇게 해줘야한다는게 중요하다! 

age와 power가 같은 것 중에 최소값을 구하는 거니까! 



그러기 위해서 [셀프 조인](https://kimsyoung.tistory.com/entry/SELF-JOIN-%E4%B8%8A-%EA%B0%99%EC%9D%80-%ED%85%8C%EC%9D%B4%EB%B8%94%EC%9D%84-%EC%A1%B0%EC%9D%B8%ED%95%98%EA%B8%B0)을 해준다. 

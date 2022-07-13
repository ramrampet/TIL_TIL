#### [많이 주문한 테이블 찾기](https://solvesql.com/problems/find-tables-with-high-bill/)

```
SELECT * 
FROM tips
WHERE total_bill > (SELECT AVG(total_bill) FROM tips)
```

#### [레스토랑의 대목](https://solvesql.com/problems/high-season-of-restaurant/)

```
SELECT *
FROM tips 
WHERE day IN ( SELECT day
               FROM tips 
               GROUP BY day 
               HAVING SUM(total_bill) >=1500)
```

**다중 서브 쿼리**

#### [레스토랑의 요일별 VIP](https://solvesql.com/problems/restaurant-vip/)

```
SELECT *  
FROM tips 
WHERE (day,total_bill) IN ( SELECT day
                                 , MAX(total_bill) as max_bill 
                            FROM tips 
                            GROUP BY day
                          )
```

#### **배운점, 인사이트** 

\- WHERE절에 집계함수 못쓰고 필요하면 서브쿼리 써야하는 거 자나 깨나 잊지 말기

\- 한동안 제주도 다녀온다고 블로그 관리를 소홀히 했다. 코드는 꾸준히 짜야하는 것! 

\- 쉬운 것도 꾸준히해야한다. 푼 문제 다시 풀기 

\- 다중 서브쿼리!! HAVING에 집계함수 쓰는 것 가능!

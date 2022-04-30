[해커랭크] Top Earners 다시 풀어보기 

![image](https://user-images.githubusercontent.com/89775352/166095962-b4b58151-7630-4505-84ce-5ff1beb31d9b.png)

내가 푼 것 
```sql
SELECT salary*months as earnings,COUNT(name)
FROM Employee
GROUP BY earnings
ORDER BY earnings DESC 
LIMIT 1
```
강사님이 푼 것 (서브쿼리)
```sql
-- Where절 서브쿼리 
SELECT months*salary AS earnings, COUNT(*)
FROM employee
WHERE months*salary=(SELECT MAX(months*salary) FROM employee)
GROUP BY earnings;
```

왜 서브쿼리를 써줘야 하는 걸까..



배운점
- 문제를 정확히 파악하는데 시간이 오래 걸렸다. 문제를 정확히 읽고 빨리 파악하는 능력을 기르자! 
- sql 문제 매일 안풀면 감이 죽는다. 꾸준히 풀자! 
- 해커랭크 리더보드에서 다른 사람들의 코드를 볼 수 있다는 것을 이제야 알았다..

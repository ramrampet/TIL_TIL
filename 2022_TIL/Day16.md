HackerRank [The Report](https://www.hackerrank.com/challenges/the-report/problem?isFullScreen=true)
```sql
SELECT CASE WHEN Marks < 70 then NULL ELSE NAME END
      ,(CASE WHEN Marks BETWEEN 0 AND 9 THEN 1
           WHEN Marks BETWEEN 10 AND 19 THEN 2
           WHEN Marks BETWEEN 20 AND 29 THEN 3
           WHEN Marks BETWEEN 30 AND 39 THEN 4
           WHEN Marks BETWEEN 40 AND 49 THEN 5
           WHEN Marks BETWEEN 50 AND 59 THEN 6
           WHEN Marks BETWEEN 60 AND 69 THEN 7
           WHEN Marks BETWEEN 70 AND 79 THEN 8
           WHEN Marks BETWEEN 80 AND 89 THEN 9
           WHEN Marks BETWEEN 90 AND 100 THEN 10
           END)grade      
      ,Marks
FROM Students
ORDER BY grade DESC, name
```
- ORDER BY 를 여러개, ASC/ DESC 둘다 쓰고 싶을 때 나눠서 쓰기 

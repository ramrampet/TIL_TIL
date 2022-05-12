HackerRank [The Report](https://www.hackerrank.com/challenges/the-report/problem?isFullScreen=true)
- 나의 풀이 
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
- 이렇게 grade 테이블을 조인해주지 않고 case로 썼다.

[다른 분의 풀이](https://mjs1995.tistory.com/113)

![image](https://user-images.githubusercontent.com/89775352/168024821-b2324e12-c8a6-4437-b022-e803f63ad5a9.png)
- 이게 더 짧고 성능이 좋은 것 같다.
- 답을 냈다고 그치지말고 다른 사람의 풀이와 비교하며 성능 비교하기! 그런점에서 리트코드가 더 좋은 점이 있다. 

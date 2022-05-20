[\[HackerRank\] Placements 문제 풀이 mysql](https://www.hackerrank.com/challenges/placements/problem?isFullScreen=true)
​
```sql
SELECT s.name as name
FROM Students s 
     JOIN Friends f ON f.id=s.id
     JOIN Packages p ON p.id=s.id
     JOIN Packages p2 ON f.friend_id=p2.id
WHERE p2.salary > p.salary     
ORDER BY p2.salary
```
​
정말 빠르고 쉽게 풀었다.

​
실력이 늘고 있는게 느껴진다. 뿌듯하다! 
​
- SQL 스터디로 다양한 문제 풀이 보강

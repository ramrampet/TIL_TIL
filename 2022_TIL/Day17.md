[\[HackerRank\] Top Competitors 문제 풀이 mysql](https://www.hackerrank.com/challenges/full-score/problem?isFullScreen=true)
```sql
SELECT h.hacker_id,h.name
FROM Submissions AS s
JOIN Challenges AS c ON c.challenge_id = s.challenge_id
JOIN Difficulty AS d ON d.difficulty_level=c.difficulty_level
JOIN Hackers AS h ON h.hacker_id=s.hacker_id 
WHERE s.score=d.score
GROUP BY h.hacker_id,h.name
HAVING COUNT(s.challenge_id)>1
ORDER BY COUNT(s.challenge_id) DESC,hacker_id
```
[more than]

- 데이터 문해력 책 읽기
- 해커랭크 두문제 풀기 (꾸준히 코드 공부하기)
- sqld 공부하기

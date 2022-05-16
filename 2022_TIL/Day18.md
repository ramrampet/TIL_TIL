[\[HackerRank\] Top Competitors 문제 풀이 mysql](https://www.hackerrank.com/challenges/full-score/problem?isFullScreen=true)

```sql
SELECT DISTINCT h.hacker_id,h.name
FROM Submissions AS s
JOIN Challenges AS c ON c.challenge_id = s.challenge_id
JOIN Difficulty AS d ON d.difficulty_level=c.difficulty_level
JOIN Hackers AS h ON h.hacker_id=s.hacker_id 
WHERE s.score=d.score;
ORDER BY c.challenge_id DESC
```

more than  = greater than = 초과  
more than or equal to = 이상
​
그렇구나.. more than 을 ~ 이상 이라고 하는 건 **한국말로 해석상** 그런 것 뿐이래! 

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
​
그렇다면 이렇게 할 수 있다.
​
**Q:  어 잠시만 Where 절에는 알리아스 못쓴다고 했던것 같은데,** 테이블 AS 라서 가능한가
​
- SELECT절에 사용된 alias라면 WHERE 절에서 사용할 수 없지만, FROM절 서브쿼리를 통해 생성된 테이블의 컬럼 이기 때문에 WHERE절에서 사용이 가능합니다. 
- 즉, 질문 주신 WHERE절의 **dr은 alias가 아니며, FROM절 테이블의 컬럼** 이기에 사용 가능한 것입니다. \[인프런 질문 답변 참고\]
- 아..그러니까 s랑 d는 알리아스가 아니라 테이블 컬럼 이라서 가능한 것! 
​

​

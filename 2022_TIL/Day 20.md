[\[HackerRank\] Challenges](https://www.hackerrank.com/challenges/challenges/problem?isFullScreen=true)

> Julia asked her students to create some coding challenges. **Write a query to print the hacker\_id, name, and the total number of challenges created by each student.** Sort your results by the **total number** of challenges in **descending** order. If more than one student created the same number of challenges, then sort the result by hacker\_id. **If more than one student created the same number of challenges** and the count is less than the maximum number of challenges created, then exclude those students from the result.

- 여기서 각각의 학생이 만든 챌린지의 수 (total number of challenges created by each student) 를 정렬하는 column이 핵심이다. 
- 조건은 그 number가

 1) 전체 학생들이 만든 챌린지수 중 Max 이거나 = MAX() 

 2) 그 number가 하나만 있어야 한다 = COUNT()=1 아니면 제거 


#### 그러면 사고의 흐름을 따로 떼어서 코드를 작성해보자. 

일단

**1) MAX** 인 값 --> 값이 하나다. 

```sql
SELECT MAX(l.num)
FROM( SELECT hacker_id, COUNT(challenge_id) as num
      FROM challenges
      GROUP BY hacker_id   
     )l
```

**2) COUNT=1** 이어야함

- 그런데 여기서 주의할 점은 '문제 풀이한 숫자가 다 각각 다른 넘버여야한다' 는 점에서 COUNT(\*)=1 이어야 한다는 것. 

만약 이렇게 해서 

```sql
SELECT hacker_id, COUNT(challenge_id) as num
FROM challenges
GROUP BY hacker_id
HAVING COUNT(challenge_id)=1
```

넣으면 

```
HAVING created = 1
```

이거랑 다를 바가 없다.

**\- 알리아스를 길어도 이해하기 쉽게 쓰기** 

  (어려운 문제 풀 때는)

이게 created challenge number가/ 하나만 있는/ num

```sql
SELECT only_one.chalnum 
FROM(SELECT b.creatednum AS chalnum
   , COUNT(b.hacker_id) AS same_num_student
     FROM (SELECT hacker_id
         , COUNT(challenge_id) as creatednum
           FROM challenges
           GROUP BY hacker_id)b
      GROUP BY b.creatednum
      HAVING same_num_student = 1
      )only_one
```

\--> 이 숫자만큼 문제를 만든 학생은 한명 밖에 없다 는 뜻. 

\--> MAX와 다르게 결과값이 여러개 --> IN 을 써야함

**이제 1번과 2번을 합쳐서 쿼리를 적으면** 

```sql
SELECT h.hacker_id
     , h.name
     , COUNT(*) AS created 
FROM hackers h
JOIN challenges c ON c.hacker_id= h.hacker_id
GROUP BY h.hacker_id, h.name
HAVING created IN (SELECT only_one.chalnum 
                    FROM(SELECT b.creatednum AS chalnum
                       , COUNT(b.hacker_id) AS same_num_student
                         FROM (SELECT hacker_id
                             , COUNT(challenge_id) as creatednum
                               FROM challenges
                               GROUP BY hacker_id)b
                          GROUP BY b.creatednum
                          HAVING same_num_student = 1
                          )only_one)
    OR created = (SELECT MAX(l.num)
                  FROM( SELECT hacker_id
                      , COUNT(challenge_id) as num
                        FROM challenges
                        GROUP BY hacker_id   
                       )l)
ORDER BY created DESC, h.hacker_id ASC
```

> 진짜 이렇게 세상 기쁠 수가 없다 ㅋㅋㅋ 😂🎁💖🚀🌟  

![image](https://user-images.githubusercontent.com/89775352/168977412-00fa58a3-fa39-42e5-ae37-3974df1d5573.png)

#### + SQL 스터디로 풀이 방법 더 적기

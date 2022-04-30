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
해결! :  https://sowhatmylifeismine.tistory.com/124


배운점
- 문제를 정확히 파악하는데 시간이 오래 걸렸다. 문제를 정확히 읽고 빨리 파악하는 능력을 기르자! 
- sql 문제 매일 안풀면 감이 죽는다. 꾸준히 풀자! 
- 해커랭크 리더보드에서 다른 사람들의 코드를 볼 수 있다는 것을 이제야 알았다..
- 서브쿼리를 안하고 HAVING절에서 MAX를 해주면 그룹바이 어닝 각각의 맥스, 즉 본인을 출력한다. 

그 외 한 것들, 배운점, 느낀점
- The system (구: 열정은 쓰레기다) 책을 읽었다. 실패에서 아주 많이 뽑아 먹어 버리자! 
- 미국 친구랑 카톡하다가 모르는 숙어를 알았다. play it by ear : 그때 상황 봐가면서 얘기하자
- 예문)이라 하고 친구가 보낸 카톡 Can we play it by ear then about meeting 6 or 6:30? 
- sql 주 3회 스터디 방법을 확정하고 다음주 월요일부터 하기로 했다. 나만의 루틴 만들기!
- 책의 영향을 받고, 건강의 한계를 느껴 스쿼트라도 매일 하는 루틴을 만들기로 했다. 홈트 20분을 했다. 

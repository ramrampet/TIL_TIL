## TIL
- 코딩 사전 과제를 풀고 어떤 부분이 문제였는지를 회고하고 배우는것, 실패에서 즙을 짜서 핥아먹는 것이 필요하다! 
- CONCAT 하는 것 
```sql
SELECT CONCAT(name, '(',LEFT(Occupation,1),')')
FROM OCCUPATIONS
ORDER BY name

SELECT CONCAT('There are a total of ',COUNT(name),' ',LOWER(occupation),'s.')
FROM OCCUPATIONS
GROUP BY occupation
ORDER BY COUNT(name), occupation
```
- 패인 분석 :from 절에 서브쿼리 인라인뷰가 보통이다. 
- select에 쓰는  서브쿼리—> 서브쿼리 , 성능이 좋지 않아 지양함. 내가 이상한 쿼리를 씀.
- IN절에 쓰는 서브쿼리는 Where가 함께, 그것도 앞의 컬럼 데이터가 뒤 데이터와 같을 때 쓴다고 한다. 

```sql
select (case when a.fi=0 then 0 else 1 end)visit_group
      ,COUNT(user_id)
from (
		select user_id 
		      ,SUM(case when device_type in ('a','i') then 1 else 0 end)as fi 
		from view_log 
		group by user_id
      )a
group by visit_group
```
- 이렇게가 맞지, 그 전에 풀었던 것도 다시 알맞은 풀이 분석하고 패인 분석하기!
- SQL 스터디를 했다. 많은걸 배웠다!

```sql
elect avg(aa.cnt) 
from   (
		select v2.user_id,count(*)as cnt
		from visit_log v2 
		where v2.user_id in(
						select user_id  
						from view_log 
						group by user_id
						having SUM(case when device_type in ('a','i') then 1 else 0 end)>0
		                   ) 
		      and v2.device_type ='w' and v2.page_id='홈' 
		group by v2.user_id         
		)aa
```    
- session id를 집계해주면 당연히 안되지 시간 없다고 막 썼네..!! (물론 그전 이야기)
- 해커랭크 SQL 5 stasrs 뱃지를 얻었다!


## 감사일기 

- 나: SQL 별 다섯개 뱃지를 얻을 때 까지 열심히 코딩 문제를 푼 내가 대견하다. 멋져 감사해
- 타인: SQL 스터디원 분들이 다양한 문제를 공유해주시고 해커랭크의 풀이와 다양한 문제 풀이 방법을 공유해주셔서 감사하다. 레아가 서브웨이도 같이 가고 전주에서
- 초코파이를 사서 선물로 나한테 포항까지 들고왔다! 레아에게 감사한다.
- 물질: 맛있는 서브웨이 이탈리아 BMT에 스위티 칠리,BBQ, 허니 머스타드, 후추 조합의 맛있는 샌드위치를 먹을 수 있는 돈이 있어서 감사하다. 잭허니도 감사 
- 경험: 면접 끝나고 그냥 놀뻔도 한데 카페를 가고 스터디를 하면서 꾸준히 자기개발에 힘쓰는 내 자신에게 감사한다 멋져멋져 

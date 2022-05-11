1. 해커랭크 풀이 
[\[HackerRank\] New Companies](https://www.hackerrank.com/challenges/the-company/problem?isFullScreen=true)

Find total number of employees.

그냥 읽고 풀면 얼레벌레 풀게 되어서 적으면서 완전히 분석해 보겠어요 ✌

#### **문제 & 해석** 

\- 뜻밖의 영어 공부 

conglomerate: 복합기업\_ A conglomerate is a multi-industry company (Wikipedia)

> 엠버의 복합 기업은 몇개의 새로운 회사를 얻었다. 각각의 회사는 아래의 위계를 따릅니다.   
> 아래의 테이블 스키마를 고려할때 회사\_코드, 설립자 이름, 리드 매니저의 총 숫자, 시니어 매니저의 총 숫자, 매니저의 총 숫자를 출력하는 쿼리를 짜세요.  너의 출력은 회사\_코드의 오름차순으로 정렬하세요. 

**노트:** 

\- 테이블은 중복된 기록을 포함할 거에요.

\- 회사\_코드는 문자열이야, 그래서 sorting(정렬)은 숫자(numeric)가 되면 안돼.

  예를 들어 회사\_코드가 C\_1,C\_2,C\_10야 그러면 오름차순 회사\_코드는 **C\_1, C\_10, C\_2** 여야해

🔍잠시만..뭐라고?

그러니까..C\_1, C\_2 에서 0:a 1:b , 2:c 같은 취급이니까 

**C\_1 : C\_b**

**C\_10 : C\_ba**

**C\_2 : C\_c**

```sql
SELECT c.company_code
       ,founder
       ,COUNT(DISTINCT e.lead_manager_code)
       ,COUNT(DISTINCT e.senior_manager_code)
       ,COUNT(DISTINCT e.manager_code)
       ,COUNT(DISTINCT e.employee_code)
FROM Company AS c
INNER JOIN Employee AS e ON c.company_code=e.company_code
GROUP BY c.company_code, founder
ORDER BY c.company_code
```
2. SQL 스터디
3. 면접 경험, 개발자 커리어로 확고하게 가자. 데이터 분석 업무 썼다고 다 데이터 분석을 하는 것이 아니다.

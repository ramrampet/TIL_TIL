## TIL 

[1141. User Activity for the Past 30 Days I](https://leetcode.com/problems/user-activity-for-the-past-30-days-i/)
​
데이터 설명 중 
​
> There is no primary key for this table, it may have duplicate rows. The activity\_type column is an ENUM of type ('open\_session', 'end\_session', 'scroll\_down', 'send\_message'). The table shows the user activities for a social media website. Note that each session belongs to exactly one user.
​
**enum은 열거형(enumerated type)**이라고 부른다. 열거형은 **서로 연관된 상수들의 집합**이라고 할 수 있다. 
​
[https://opentutorials.org/course/2517/14151](https://opentutorials.org/course/2517/14151 "출처")
​
```sql
SELECT  activity_date AS day 
       ,COUNT(DISTINCT user_id) as active_users
FROM Activity 
WHERE (activity_date BETWEEN '2019-06-28' AND '2019-07-27')
      AND activity_type IS NOT NULL 
GROUP BY activity_date
```
​
매번 풀던 거라 코드는 매우 간단하게 풀었다. 

​
​
```sql
select activity_date as day, count(distinct user_id) as active_users 
from Activity
where datediff('2019-07-27', activity_date) <30
group by activity_date
```
​
이풀이도 비슷하지만 datediff..

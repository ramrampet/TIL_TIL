[일별 블로그 방문자 수 집계](https://solvesql.com/problems/blog-counter/)

```sql

SELECT event_date_kst as dt 
     , COUNT(DISTINCT user_pseudo_id) as users 
FROM ga 
WHERE (event_name IS NOT NULL) 
    AND event_date_kst BETWEEN '2021-08-02'AND '2021-08-09' 
GROUP BY event_date_kst
ORDER BY dt ASC 
```

날짜 붙일때, 문자열이니까 '' 붙이는거 있지 말고, AND로 이어줄 때 우선순위 바뀔 수 있으니까 () 잘 넣어주기 

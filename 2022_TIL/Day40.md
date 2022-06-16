```sql
SELECT COUNT(DISTINCT user_pseudo_id, ga_session_id)total
      ,(COUNT(DISTINCT user_pseudo_id, ga_session_id) 
      -(SELECT COUNT(DISTINCT user_pseudo_id, ga_session_id)
        FROM ga 
        WHERE event_name='page_view' 
              AND page_title='백문이불여일타 SQL 캠프 입문반'))pv_no
      ,(SELECT COUNT(DISTINCT user_pseudo_id, ga_session_id)
        FROM ga 
        WHERE event_name='page_view' 
              AND page_title='백문이불여일타 SQL 캠프 입문반')pv_yes
FROM ga
```

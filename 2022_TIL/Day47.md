## TIL 
SQL 데이터 분석 캠프 실전반 전환율 (퍼널 분석)
-      서브 쿼리로 풀다보니 서브 쿼리의 서브 쿼리,,,, 이런식으로 너무 복잡해질 것 같아 WITH를 쓰기로 했다.
-   저번 스터디 시간에 들은 건데, WITH가 현업에서 가독성도 좋고 성능도 좋아 많이 선호된다고 한다.

```sql
WITH pv AS (
SELECT user_pseudo_id,ga_session_id,event_name,page_title      
       ,event_timestamp_kst
FROM ga 
WHERE page_title= '백문이불여일타 SQL 캠프 실전반'
AND event_name = 'page_view'
)
​
,scroll AS (
SELECT user_pseudo_id,ga_session_id,event_name,page_title          
      ,event_timestamp_kst
FROM ga 
WHERE page_title= '백문이불여일타 SQL 캠프 실전반'
AND event_name = 'scroll'
) 
​
,click AS (
SELECT user_pseudo_id,ga_session_id,event_name,page_title
      ,event_timestamp_kst
FROM ga 
WHERE event_name = 'SQL_advanced_form_click'
)
​
SELECT pv
      ,scroll_after_pv
      ,click_after_scroll
      ,ROUND((scroll_after_pv/pv),3)pv_scroll_rate
      ,ROUND((click_after_scroll/pv),3)pv_click_rate
      ,ROUND((click_after_scroll / scroll_after_pv),3)scroll_click_rate
FROM
    (SELECT COUNT(DISTINCT pv.user_pseudo_id,pv.ga_session_id)pv
      ,COUNT(DISTINCT scroll.user_pseudo_id,scroll.ga_session_id)scroll_after_pv
      ,COUNT(DISTINCT click.user_pseudo_id,click.ga_session_id)click_after_scroll
FROM pv
     LEFT JOIN scroll ON pv.user_pseudo_id=scroll.user_pseudo_id              
            AND pv.ga_session_id=scroll.ga_session_id
            AND scroll.event_timestamp_kst >= pv.event_timestamp_kst
     LEFT JOIN click ON pv.user_pseudo_id=click.user_pseudo_id                 
            AND pv.ga_session_id=click.ga_session_id
            AND click.event_timestamp_kst >= scroll.event_timestamp_kst
      )p
```
​
#### **인사이트** 
​
-   WITH a AS(), WITH b AS() 이렇게 안쓰고 WITH a as(), b() 이렇게 써도 된다! 앞에 with가 받아준다. 
-   테이블을 여러개 만들 때, 각 테이블 값의 속성으로 간단하게 만들어 외우지 않아도 되게 만들기 
-   DISTINCT 잡아줘야하니까 조인 조건 여러개 걸기 
-   LEFT JOIN으로 조건 잘라서 걸어주니까 SELECT절에 과도한 부담이 가지 않아 성능에 좋다. 
-   From절 서브쿼리 하나라서 테이블 호출 안해주더라도 이름은 지어주는거 명심 
-   오타 주의~ 자나 깨나 오타 확인~

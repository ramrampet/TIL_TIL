### 감사일기
- 나: 오늘 친구들이랑 축구를 보러간건 좋은 선택이었다. 좋은 선택을 한 나에게 감사해 
- 타인: 오늘 친구들이 나와 같이 맛있는 타코와 닭꼬치를 먹어서 너무 감사하다
- 물질: 돈 안벌어도 살수있는 나 감사해
- 경험: 진지한 고민을 같이 나눌 수 있는 친구를 쌓은 것에 




### TIL
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



SELECT COUNT(DISTINCT user_pseudo_id, ga_session_id)total
      ,(COUNT(DISTINCT user_pseudo_id, ga_session_id) 
      -(SELECT COUNT(DISTINCT user_pseudo_id, ga_session_id)
        FROM ga 
        WHERE event_name='page_view' 
              AND page_title='백문이불여일타 SQL 캠프 입문반'))pv_no
      ,(
        (SELECT COUNT(DISTINCT user_pseudo_id, ga_session_id)
        FROM ga 
        WHERE event_name='page_view' 
              AND page_title='백문이불여일타 SQL 캠프 입문반')
       - (SELECT COUNT(DISTINCT user_pseudo_id, ga_session_id)
        FROM ga
        WHERE ga_session_id IN  (SELECT ga_session_id 
                                 FROM ga 
                                 WHERE event_name='page_view' 
                                 AND page_title='백문이불여일타 SQL 캠프 입문반')
        AND event_name='scroll' 
        AND page_title='백문이불여일타 SQL 캠프 입문반'))pv_yes_scroll_no        
      ,(SELECT COUNT(DISTINCT user_pseudo_id, ga_session_id)
        FROM ga
        WHERE ga_session_id IN  (SELECT ga_session_id 
                                 FROM ga 
                                 WHERE event_name='page_view' 
                                 AND page_title='백문이불여일타 SQL 캠프 입문반')
        AND event_name='scroll' 
        AND page_title='백문이불여일타 SQL 캠프 입문반'  )pv_yes_scroll_yes
FROM ga



```

#### 배운점, 인사이트 
- 굳이 알리아스 로 연산하려고 애써서 서브쿼리 만들지 말기

- 편리한 SELECT 절 서브쿼리 쓰는 법에 능숙해지기 

- SELECT DISTINCT 뒤에 컬럼 두개 쓰는 것!

- 연습에서는 왜 그런지 많이 고민해보되 실전에서는 바로 다른 풀이로 풀어보기!

- 쿼리 결과값을 알 수 있다면, 여기서 수가 적어지는지, 많아지는지를 파악하여 오답 원인의 힌트를 얻을 수 있다!

- 역시 이 로그 데이터와 가장 유사한 테이블이 코딩 테스트에 가장 많이 나오는 데이터 유형! 많이 변형하여 공부하기

- 성능을 고민하며 풀이하는 것이 역시 제일 관건인 것 같다!, -> sql 스터디가 필요한 이유

- 모르겠는것, 이해안되는 것 그냥 얼레벌레 넘어가지 말고 스터디 시간을 최대한 활용하여 다양한 문제풀이 얻어가기!

- 스터디장이 늦거나 환경에 문제가 있으면 안되겠죠? 그리고 어떤 일이 있어도 주 3회 SQL 스터디를 유지하는 것 중요, 언제나 관건은 핵심 역량! 

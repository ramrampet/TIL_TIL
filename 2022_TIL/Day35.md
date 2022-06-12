## 감사일기 
- 나: 자전거를 타면서 행복감을 느낀 나에게 감사합니다. 자전거를 탈 수 있는 건강한 두다리! 
- 타인: 레아가 내일 줄게 있다고 했다. 아마 선물인것 같다 :) 행복감을 주는 레아에게 감사합니다. 오늘 면접 스터디 했던 분들이 나의 블로그 글을 보고 뭘해도 될 분! 이라고 말해 주셨다. 헤헤 감사합니다.
- 물질: 비교적 최신 노트북을 가진다는 감사함을 잊고 산것 같다. 감사합니다. 
- 경험: 더 시스템이라는 좋은 책을 완독할 수 있게 해주셔서 감사합니다! 

## TIL

**한문제 한문제 잘근 잘근 씹어먹기\_SQL 성장기 🌟**

[지역별 주문의 특징](https://solvesql.com/problems/characteristics-of-orders/)

**의문점 \[해결\]**  왜 order\_id를 DISTINCT 처리해줘야하는 걸까?

테이블마다 그 이유는 달랐지만 대부분 order\_id를 DISTINCT 해줘야 했다.

이번 테이블에서는 한 order\_id에 다양한 category, procuct\_id가 있지만 몇개를 구매하든 '주문량'을 구해야하는 것임으로 distinct를 해주는 게 맞다고 이해했다. pivot table을 해주기에.   

![image](https://user-images.githubusercontent.com/89775352/173234555-e67b92f9-6547-43c3-8aec-d5836ba97e9a.png)
```sql
SELECT Region
,COUNT(DISTINCT CASE WHEN category='Furniture' then order_id END) as Furniture
,COUNT(DISTINCT CASE WHEN category='Office Supplies' then order_id END) as 'Office Supplies'
,COUNT(DISTINCT CASE WHEN category='Technology' then order_id END) as Technology
FROM records
GROUP BY Region
ORDER BY Region
```

**배운점**

-   order\_id 는 보통 카테고리, product\_id 등이 달라도 distinct하게 해서 주문 수를 세주는게 맞다.
-   Pivot table 해줄 때 컬럼명을 띄어쓰기 포함해서 지정해 주려면 ' '를 붙여야한다. 아니면 에러가 난다. 

[가구 판매의 비중이 높았던 날 찾기](https://solvesql.com/problems/day-of-furniture/)

**풀이 1.** 처음 내 풀이 

```sql
 SELECT s.order_date as order_date
       ,s.f as furniture
       ,ROUND(s.f/(s.f+s.l)*100,2) as furniture_pct
 FROM (
      SELECT order_date
          ,COUNT(CASE WHEN category='Furniture' THEN order_id END) as f
          ,COUNT(CASE WHEN category<>'Furniture' THEN order_id END) as l
      FROM records 
      GROUP BY order_date
      HAVING (f+l)>=10 
      )s
  WHERE ROUND(s.f/(s.f+s.l)*100,2)>=40    
  ORDER BY furniture_pct DESC
```

- 백분율이라서 100을 안 곱해줘서 그런 줄 알았는데, 곱해줘도 쿼리 결과가 달랐다. (쿼리 결과: 10개, 정답: 12개)

- 다른 분들의 풀이와 비교해보니 너무 이상하게 푼 것 같다.  이유: 알리야스를 지정해 쉽게 연산하고 싶었다. (흐유)

**의문점 \[미해결\]** - 사실 아직까지 왜 답이 안나오는지 명확하게 설명을 못하겠다. 쿼리 결과를 비교하면서 알아봐야지

**풀이 2.** 내 풀이 + 다른 분 풀이 

```sql
SELECT order_date
  ,COUNT(DISTINCT CASE WHEN category = 'Furniture' THEN order_id END) 
   AS furniture 
  ,ROUND((COUNT(DISTINCT CASE WHEN category = 'Furniture' THEN order_id END)
   /COUNT( DISTINCT order_id))*100,2) as furniture_pct 
FROM records
GROUP BY order_date
HAVING COUNT(DISTINCT order_id) >= 10 AND furniture_pct >=40
ORDER BY furniture_pct DESC, order_date
```

 - 정답! , 정말 서브 쿼리 쓸 필요 없었는데.. 


- 스터디 시간에 같이 해결해보도록 하자.

**풀이 3**. 스터디원분 풀이 

```
SELECT order_date
     , COUNT(DISTINCT IF(category = 'Furniture', order_id, NULL)) furniture
     , ROUND(COUNT(DISTINCT IF(category = 'Furniture', order_id, NULL))*100 
       / COUNT(DISTINCT order_id), 2) furniture_pct
FROM records
GROUP BY order_date
HAVING COUNT(DISTINCT order_id) >= 10
AND furniture_pct >= 40.0
ORDER BY furniture_pct DESC, order_date
```

\- IF 문을 쓰셨다. 나는 IF문을 거의 쓰지 않아서 몰랐는데, 이번 기회에 다시 배워보도록하자. 

![image](https://user-images.githubusercontent.com/89775352/173234592-252fd8d3-3951-4321-bf17-651b56fce51b.png)

\- CASE 문과 논리는 같은데 더 간단하게 쓸 수 있는 것 같다.

**풀이 4**. 스터디원분 풀이 

![image](https://user-images.githubusercontent.com/89775352/173234600-ad512c6d-4977-499d-b8f1-f804f574d338.png)

\- 위의 풀이 3과 같은데 Where절에서 데이터 용량을 끊어주면 성능이 높아진다는 것에 착안하셔서 코드를 짜셨다고 한다.

  데이터 수가 많을 때하면 정말 좋을듯! 

**배운점** 

-    ID를 SUM을 해주면 안되지 COUNT해줘야지!
-   IF(조건,참일때 반환,거짓일 때 반환)
-   계산식 집계함수 써서 길어진다고 서브쿼리로 더 복잡하게 하는 건 정말 아니야... 
-   다양한 문제 풀이 방법과 성능 향상을 고민해봐야지 비로소 나의 헛점을 깨닫고 더 성장할 수 있다. 

[작품이 없는 작가 찾기](https://solvesql.com/problems/artists-without-artworks/)

```sql
SELECT aa.artist_id as artist_id
      ,aa.name as name 
FROM artists aa
WHERE aa.artist_id NOT IN  
                     (SELECT DISTINCT a.artist_id
                      FROM artworks_artists as w
                      JOIN artists a ON a.artist_id=w.artist_id)
      AND aa.death_year IS NOT NULL
```

\- 쉽네! 라고 생각했다. 그런데 또... 정말 쓸데 없이 서브 쿼리를 쓰는 거 왜그런거죠..? 

(스터디원분 풀이)

![image](https://user-images.githubusercontent.com/89775352/173234618-ed41141e-8f50-48bd-a398-6239a8f5aa36.png)


하하 ㅎㅎㅎ 

**배운점**

-   서브 쿼리 못잃어 병 걸린 것 같다.
-   혼자 풀고 넘어갔으면 무조건 히히 하고 문제 없어! 했을듯.. 역시 이렇게 다양한 문제풀이를 비교해봐야 해!

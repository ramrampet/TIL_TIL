## TIL 
- 구글 애널리틱스 강의를 들었다.
- 적응했다. 

[카테고리 별 매출 비율](https://solvesql.com/problems/revenue-pct-per-category/)
- 왜 두개의 컬럼(category,sub_category)이 아니라 category에만 DISTINCT를 해줘도 중복 열이 사라질까. 
```sql
SELECT DISTINCT category 
      ,sub_category
      ,ROUND(SUM(sales) OVER(PARTITION BY category,sub_category),2)sales_sub_category
      ,ROUND(SUM(sales) OVER(PARTITION BY category),2)sales_category
      ,ROUND(SUM(sales) OVER(),2)sales_total
      ,ROUND(SUM(sales) OVER(PARTITION BY category,sub_category)/SUM(sales) OVER(PARTITION BY category)*100,2)pct_in_category
      ,ROUND(SUM(sales) OVER(PARTITION BY category,sub_category)/SUM(sales) OVER()*100,2)pct_in_total
FROM records
```
- %일 때 100 곱해주는 거 까먹지 말기 

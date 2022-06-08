### TIL
```sql
SELECT Region
,COUNT(CASE WHEN category='Furniture' then order_id END) as Furniture
,COUNT(CASE WHEN category='Office Supplies' then order_id END) as OfficeSupplies
,COUNT(CASE WHEN category='Technology' then order_id END) as Technology
FROM records
GROUP BY Region
ORDER BY Region
```
https://solvesql.com/problems/characteristics-of-orders/
- Retention 의 개념, Classic retention은 N day retention이라고 많이 불립니다. 예를 들어 10명의 이용자가 앱을 처음 이용하였고 6명이 7일안에 다시 방문하였다면 
  day 7 리텐션은 60%가 됩니다.
- range retention은 7일-10일 사이의 범위를 보기 때문에 그러한 클래식 리텐션의 측정일에 대한 노이즈를 보완할 수 있습니다.

- 면접 준비, 그로스해킹

### 감사할거리  
- 나: 좌절할 일이 많았지만 굴하지 않고 끝까지 열심히 하는 자세를 끝내 잃지 않은 나에게 감사합니다. 
- 타인: 아버지가 해뜨기 전이 가장 어둡다고 말씀해 주시고 어머니가 하트를 날려주셨다. 화목한 가정에 태어나게 해주신 부모님께 감사합니다. 
- 물질: 오늘 카페에서 커피를 쏟아서 직원분께 죄송하다고 말씀드렸는데, 커피를 새걸로 가져다 주셨다. 직원분의 사소한 배려에 정말 감사했다.  
- 경험: 호인가 면접 준비를 도와줘서 큰 도움이 되었다. 호인이에게 감사한다. 

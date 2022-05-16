### 2022 05 03
- 해커랭크 The Blunder
 
![image](https://user-images.githubusercontent.com/89775352/166382019-e3e16a14-8da6-4d27-815b-95b8e73cade9.png)
![image](https://user-images.githubusercontent.com/89775352/166384241-61812f14-eb18-4aad-a504-7ce50f94dfdb.png)

1. 
```sql
-- Write a query calculating the amount of error 
SELECT CEIL(
        AVG(salary)-AVG(REPLACE(salary,0,''))
            )
FROM EMPLOYEES
```
- 집계함수를 쓰지만 여기서 GROUP BY를 쓸 필요는 없다 값을 하나를 내고, 마지막에 CEIL을 붙여준다


- SQLD 강의 들으면서 기초 다시 복습 

### 배운점
- 나 왜이렇게 못하지..어렵지... 가 아니라 당연한거다. 정도는 없다. 당연히 거쳐야할 것을 겪으며 성장하는 중!
- 막연할 때는 의사코드 적기 

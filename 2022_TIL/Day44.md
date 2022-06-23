[185. Department Top Three Salaries](https://leetcode.com/problems/department-top-three-salaries/)

(1) 나의 풀이 

```
SELECT d.name as Department 
      ,a.name as Employee
      ,a.salary as Salary
FROM   (
        SELECT id
              ,name
              ,salary
              ,departmentid
              ,DENSE_RANK() OVER (PARTITION BY departmentId ORDER BY salary DESC)rank
        FROM Employee 
        )a
JOIN Department d ON a.departmentid=d.id
WHERE a.rank <4
```

\- 한번에 풀었다 ! 호호 

[(2) 다른 풀이](https://leetcode.com/problems/department-top-three-salaries/discuss/53692/Accepted-solution-without-group-by-or-order-by) 

[##_Image|kage@rdImR/btrFuEcFBF5/I4NvErTX4z7TygqQhX9GJ1/img.png|CDM|1.3|{"originWidth":745,"originHeight":430,"style":"alignLeft"}_##]

#### **배운점, 인사이트** 

\- dense\_rank를 생각해내고 이걸 서브 쿼리로 묶는게 포인트 아이디어를 내는게 관건이었던 것 같다. 

\- dense ransk  partition by 생각해낸 것이 좋았다. 윈도우 함수니까 MS sql에서 가능하기 때문에 mysql에서 사용하지 않도록 주의 하기 

\- 다양한 풀이가 있다는 것을 알게 되었다. 쓸데 없는 복잡한 로직은 불필요하지만 most votes 순으로 보는 것이 좋다. 

[196. Delete Duplicate Emails](https://leetcode.com/problems/delete-duplicate-emails/)

```
DELETE p1
FROM Person p1, Person p2
WHERE p1.Email = p2.Email 
      AND p1.Id > p2.Id
```

\- ID가 최소인 조건들을 고려해야 함 DELETE 함수에 익숙해질 것 

[197.Rising Temperature](https://leetcode.com/problems/rising-temperature/)

```
 SELECT a.id 
 FROM     (
            SELECT  id 
                   ,recorddate
                   ,temperature 
                   ,(LAG(temperature,1) OVER (ORDER BY recorddate))b  
            FROM Weather
           )a
WHERE a.temperature > a.b
```

\- 처음에 LEAD를 썼다가 에러가 나왔다. 이상할 때는 서브 쿼리안의 쿼리를 출력해보는게 도움이 됨! 

\- ORDER BY 와 LAG/LEAD 안의 것 분리!

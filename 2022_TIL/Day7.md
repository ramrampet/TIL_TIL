### leetcode 다시 풀기 
184. Department Highest Salary

Write an SQL query to find employees who have the highest salary in each of the departments.

Return the result table in any order.

이것이 왜 틀렸고, 어떻게 해야하냐면 
```sql
SELECT Department.name,Employee.name,MAX(salary)
FROM Employee
INNER JOIN Department ON Employee.departmentId=Department.id
GROUP BY Department.name

{"headers": ["name", "name", "MAX(salary)"],
"values": [["IT", "Joe", 90000], 
           ["Sales", "Henry", 80000]]}
```           

본인이 일단 LEFT JOIN / INNER JOIN의 차이 명확히
```sql
SELECT *
FROM Employee
LEFT JOIN Department ON Employee.departmentid = Department.id
# INNER 했을 때
# {"headers": ["id", "name", "salary", "departmentId", "id", "name"], 
#     "values": [[1, "Joe", 70000,         1,            1,  "IT"], 
#                [3, "Henry", 80000,       2,            2, "Sales"]]}

# LEFT 했을 때 
{"headers": ["id", "name", "salary", "departmentId", "id", "name"], 
    "values": [[1, "Joe", 70000, 1, 1, "IT"], 
               [2, "Jim", 90000, 1, 1, "IT"], 
               [3, "Henry", 80000, 2, 2, "Sales"], 
               [4, "Sam", 60000, 2, 2, "Sales"], 
               [5, "Max", 90000, 1, 1, "IT"]]}
```               
답
```sql
SELECT d.name AS department,e.name AS employee,e.salary
FROM employee AS e
     INNER JOIN(
    SELECT departmentid,MAX(salary) AS max_salary 
    FROM employee
    GROUP BY departmentid
    )AS dh ON e.departmentid=dh.departmentid
        AND e.salary =dh.max_salary
    INNER JOIN department AS d ON d.id=e.departmentid
    #depart 이름 이렇게 붙여줌 
```

다시 풀어보기! 

- A/B TEST / Yammer
- 뜻밖의 영어 공부, triage : 부상자 분류인데 여기서는 분류 
ex) Yammer's Analysts are responsible for triaging product and business problems
- fire () up : -를 작동시키다. 

![image](https://user-images.githubusercontent.com/89775352/166148736-ed5244c4-7433-41ee-9533-e77c47e9d0e1.png)


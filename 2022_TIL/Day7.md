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

본인이 일단 LEFT JOIN / INNER JOIN의 차이를 아직 헷갈려함 
그러니까 ID 같은걸 기준으로 조인했는데 왜 LEFT..?
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

[leetcode] 627. Swap Salary

Write an SQL query to swap all 'f' and 'm' values (i.e., change all 'f' values to 'm' and vice versa) with a single update statement 
and no intermediate temporary tables.
```sql
UPDATE salary 
SET sex = CASE WHEN sex= 'f' THEN 'm' ELSE 'f' END
```

![image](https://user-images.githubusercontent.com/89775352/165455322-1fb94f07-405f-470f-93e4-7e003a902eb3.png)

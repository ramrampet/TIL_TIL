## hacker rank _ OCCUPATIONS
Pivot the Occupation column in OCCUPATIONS so that each Name is sorted alphabetically and displayed underneath its corresponding Occupation. The output column headers should be Doctor, Professor, Singer, and Actor, respectively.

Note: Print NULL when there are no more names corresponding to an occupation.

Input Format

The OCCUPATIONS table is described as follows:


Occupation will only contain one of the following values: Doctor, Professor, Singer or Actor.
![image](https://user-images.githubusercontent.com/89775352/166239396-5a8937a7-3eb7-4524-9d2c-eef89849fec4.png)

#### 1번 전략 , PIVOT, 

![image](https://user-images.githubusercontent.com/89775352/166239255-be10a0c8-3b20-4e42-be4e-24f7c9e17873.png)

-> NULL 잔치_ 어떡하지? 


```sql
set @r1=0, @r2=0, @r3=0, @r4=0; 

select min(Doctor), min(Professor), min(Singer), min(Actor) 
from ( select case 
       when occupation = 'Doctor' then (@r1:=@r1+1) 
       when occupation = 'Professor' then (@r2:=@r2+1)
       when occupation = 'Singer' then (@r3:=@r3+1) 
       when occupation = 'Actor' then (@r4:=@r4+1) end as rowNum, 
       case when occupation = 'Doctor' then Name end as Doctor, 
       case when occupation = 'Professor' then Name end as Professor, 
       case when occupation = 'Singer' then Name end as Singer, 
       case when occupation = 'Actor' then Name end as Actor from OCCUPATIONS order by Name) as temp group by rowNum;
```
![image](https://user-images.githubusercontent.com/89775352/166256333-b480c155-406f-4565-833e-ca842f1aaecc.png)

- 스터디를 통해 많이 배웠다! 

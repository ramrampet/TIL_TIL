### 프로그래머스 SQL 
- [없어진 기록 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/59042)

```sql
SELECT O.ANIMAL_ID
      ,O.NAME 
FROM ANIMAL_OUTS AS O 
LEFT JOIN ANIMAL_INS AS I ON O.ANIMAL_ID= I.ANIMAL_ID 
WHERE I.ANIMAL_ID IS NULL 
ORDER BY O.ANIMAL_ID
-- OUTS에는 있는데 INS에는 없어
```
![image](https://user-images.githubusercontent.com/89775352/180601958-00e53af6-6793-475d-a808-0583547d946d.png)

- [있었는데요 없었습니다](https://school.programmers.co.kr/learn/courses/30/lessons/59043)
```sql
SELECT I.ANIMAL_ID
      ,I.NAME
FROM ANIMAL_INS AS I 
     LEFT JOIN ANIMAL_OUTS AS O ON I.ANIMAL_ID=O.ANIMAL_ID
     WHERE I.DATETIME>O.DATETIME
ORDER BY I.DATETIME     
```
### 이것이 코딩 테스트다 복습 
### 오늘 Greedy & 구현 끝내기!

![image](https://user-images.githubusercontent.com/89775352/180601265-5106cea3-25bb-40a6-b352-b189ff093366.png)

```python
# <문제>  곱하기 혹은 더하기 

data = input()

# 첫 번째 문자를 숫자로 변경하여 대입 
result = int(data[0])

for i in range(1,len(data)):
    num=int(data[i])
    if num <= 1 or result <= 1:
        result += num
    else: 
        result *= num
print(result)   
```
![image](https://user-images.githubusercontent.com/89775352/180601297-95fdeeac-e029-47f1-b66f-3b42452a2b64.png)
```python
# <문제> 모험가 길드 
n = int(input())
data= list(map(int,input().split()))
data.sort() 
# 오름차순으로 

result=0 # 총 그룹의 수 
count=0 # 현재 그룹에 포함된 모험가의 수 

for i  in data: # 공포도를 낮은 것부터 하나씩 확인하며 
    count+= 1 # 현재 그룹에 해당 모험가를 포함시키기
    if count >=i:
        result += 1
        count = 0
print(result)  
```
### 구현 (Implementation)
![image](https://user-images.githubusercontent.com/89775352/180602736-673b76e3-a34d-4afd-bb73-158990f07f35.png)
- 풀이를 떠올리는 것은 쉽지만 소스코드로 옮기기 어려운 문제를 지칭 
![image](https://user-images.githubusercontent.com/89775352/180602821-c4e431bd-0966-4a7d-9e30-43afb930ab22.png)

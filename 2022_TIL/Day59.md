## TIL 
- 통계, growth hacking (A/B 테스팅 등등) 에 대해서 더 공부하였다.
- 결측치를 처리하는 7가지 방법에 대해 공부하였다.
- 이코테 알고리즘 내용을 복습하였다. 


### 이코테 복습하기 

- 기본 입출력 
```python
# 공백을 기준으로 구분된 데이터를 입력 받을 때 다음과 같이 사용합니다. 
list(map(int, input().split()))

# 공백을 기준으로 구분된 데이터의 개수가 많지 않다면, 단순히 다음과 같이 사용합니다.
a, b, c = map(int, input().split())

n = int(input())
data = list(map(int,input().split()))

print(n)
print(data)
```
#### 그리디
1. 
```python
n = 1260
count = 0 

array = [500,100,50,10]
for coin in array:
  count += n// coin 
  n %= coin 

print(count)
```
2.
```python
n, k=map(int, input().split())

result = 0 

while True:
  # N이 K로 나누어 떨어지는 수가 될 때까지 빼기
  target = (n//k)*k
  result += (n - target)

  if n < k:
    break

  result += 1 
  n //=k 

# 마지막으로 남은 수에 대하여 1씩 뺘기
result += (n-1)
print(result)
```

- 위 내용은 이것이 코딩 테스트다 강의를 기반으로 작성되었습니다. 

## 감사일기 
- 나 : 노트북이 없는 상황에도 방법을 만들어 공부한 나 자신에게 감사한다 헤헤
- 타인: 화목한 가정이 있어 감사하고, 방을 잘 구해서 감사하다.
- 물질: 이 가격에 이런 환경에서 잠시나마 살 수 있다니....
- 경험: 공부하는 게 재밌다. 그래서 지금 막 행복감이 엄청 든다.. 감사해요 마이 월드!!

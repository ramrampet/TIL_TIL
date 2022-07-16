## TIL 
- 나도 코딩 파이썬을 복습하였다.

```python
# 지역변수 : 함수내에서 만 사용 , 호출이 끝나면 끝
# 전역변수 : 프로그램 내에서 어디서든지 부를 수 있는 변수 
gun= 10

def checkpoint(soldiers): # 경계근무
    global gun # 전역 공간에 있는 gun 사용 
    gun = gun - soldiers
    print("[함수 내] 남은 총: {0}".format(gun))

def checkpoint_ret(gun,soldiers):
    gun = gun - soldiers
    print("[함수 내 남은 총 : {0}".format(gun))
    return gun

print("전체 총: {0}".format(gun))
# checkpoint(2) # 2명이 경계 근무 나감 
gun = checkpoint_ret(gun,2)
print("남은 총: {0}".format(gun))

# 가변인자
def profile(name, age, *language):
    print("이름: {0}\t나이 : {1}\t".format(name,age), end=" ")
    for lang in language:
        print(lang, end=" ")
    print()

profile("유재석", 20, "Python","Java","C","C++","C#","Javascript")
profile("김태호", 25, "Kotilin","Swift")


import sys
print("Python", "Java", file=sys.stdout) #표준출력
print("Python", "Java", file=sys.stderr) #표준에러 

# 시험 성적
scores={"수학":0, "영어":50, "코딩":100}
for subject, score in scores.items():
    # print(subject, score)
      print(subject.ljust(8), str(score).rjust(4),sep=":")
```
- ljust() : 왼쪽 정렬, rjust() : 오른쪽 정렬 
- 함수 안에서 쓰는 변수, 밖에서도 통용되는 변수 등등
- 역시 복습하고 기록하지 않으면 다 까먹는다. 아는척하지 말고 헷갈리면 복습하기!
-  SQL만 요새 계속 쓰다보니 Python에서 ==인 것을 =로 쓰는 경우가 있다. 언어별 차이 주의하기

## 감사일기
- 나: 오늘 파이썬을 복습한 나에게 감사한다. 
- 타인: 집을 같이 알아봐준다는 오빠에게 감사한다.
- 물질: 공차는 사랑이다.
- 경험: 어머니에게 생신 선물을 사드릴 수 있는 경험을 할 수 있음에 감사하다. 

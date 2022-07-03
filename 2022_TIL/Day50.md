[1393. Capital Gain/Loss](https://leetcode.com/problems/capital-gainloss/)
​
**1\. 나의 풀이** 
​
```
SELECT stock_name
      ,SUM(CASE WHEN operation='Buy' THEN -price ELSE +price END) AS capital_gain_loss
FROM Stocks
GROUP BY stock_name
```
​
\- 처음에는 약간 흠.. 이렇게 생각했지만 피봇을 떠올리고 나니 명확해졌다. 
​
**2\. Most votes 풀이**
​
요즘 리트 코드를 풀고 나서는 most votes 순으로 풀이를 비교하곤 하는데, **투표 1위가 나의 풀이와 같은 경우가 많아서** **뿌듯해지고 있다.** 하지만 자만하지말고 모르는 걸 긁어 모아야지!
​
[##_Image|kage@bb9soW/btrGksvpWyw/HgxPFKmjek9Pa4zG4NjCw1/img.png|CDM|1.3|{"originWidth":621,"originHeight":476,"style":"alignCenter","width":584,"height":448}_##]
​
\+ 성능 고민 
​
이번에도 역시 똑같은 쿼리를 반복적으로 submit했을 때 계속 성능이 다르게 나왔다.
​
세번째 섭밋하니까 이런 99.51% 가 나왔다... 기뻐하는 것이 맞나..? 밑에는 똑같은 쿼리로 했을 때 runtime 이 계속 달라지는 것을 알 수 있다. 
​
[##_Image|kage@qq9fa/btrGjFhtc9K/Hsgmf7jZMVlkJARj6vWm7K/img.png|CDM|1.3|{"originWidth":707,"originHeight":753,"style":"alignCenter"}_##]
​
3\. 다른 풀이 1 
​
[ashishkjha](https://leetcode.com/ashishkjha)109
​
November 7, 2020 6:27 AM
​
Read More
​
same idea but i prefer using if/else over case for concise solution
​
```
select stock_name
, sum(if(operation = 'Buy', -1, 1) * price) as capital_gain_loss
from stocks
group by stock_name
```
​
와 역시,, 내가 상대적으로 if문을 사용하는 방법을 이용하지 않는데 ,이것도 코드가 간결한 것 같다.
​
if(조건문, 참일때, 거짓일 때)
​
4\. 다른 풀이 2 
​
[Alan418](https://leetcode.com/Alan418)
​
```
select distinct stock_name
    , sum(case when operation = 'Buy' then -price else price end) 
      over (partition by stock_name) capital_gain_loss
from stocks
```
​
와.. 윈도우 함수를 쓰는 방법도 있구나.. 이게 성능이 더 좋은가..?  리트코드 성능의 미스터리부터 풀자.
​
[1667. Fix Names in a Table](https://leetcode.com/problems/fix-names-in-a-table/)
​
1\. 나의 풀이 
​
```
SELECT user_id
      ,CONCAT(UPPER(LEFT(name,1)),LOWER(SUBSTR(name,2,10)))name
FROM Users 
ORDER BY user_id
```
​
\- 길이를 정하기에는 예시처럼 이름 길이가 명확치 않음으로 좋지 않다, substr에 길이 지정 안해주고 시작 위치만 정해줘도 작동을 하더라.
​
```
SELECT user_id
      ,CONCAT(UPPER(LEFT(name,1)),LOWER(SUBSTR(name,2)))name
FROM Users 
ORDER BY user_id
```
​
[##_Image|kage@u14vb/btrGmo7cmrH/3VZGtoLjEsKgn9qaBigSW0/img.png|CDM|1.3|{"originWidth":708,"originHeight":259,"style":"alignCenter"}_##]
​
**성능이 백프로가 나오긴 했다..!!**
​
2\. mostvotes= 풀이 같음
​
3\. 배운점 
​
문자열 자르는거 너무 상대적으로 많이 어색함 
​
LEFT(문자열/칼럼,길이) right 동일 
​
SUBSTR(문자열/칼럼,시작 위치,길이)
​
CONCAT도!

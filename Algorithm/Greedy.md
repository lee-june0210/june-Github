
# 그리디
> 그리디 알고리즘은 현재 상황에서 가장 좋은 최적의 해만 고르는 방법이다.<br>
즉, 매 순간 제일 최적의 해로 보이는 해를 선택하며 현재의 선택이 나중에 어떠한 영향을 미칠지는 고려하지 않는다. <br>
__문제를 봤을 때 단순히 현재 상황에서 가장 좋아보이는 최적의 해만 선택해도 문제를 정상적으로 풀어낼 수 있는지 파악해야한다. -> 그리디의 핵심!__

<br>
<br>

## :mega: 구명보트

```python
def solution(people, limit):
    people.sort()
    cnt = 0
    # for i in range(len(people)): # for 문 돌리는데서 out of range 문제를 해결할 수가 없었다. 
    while people :                  # 하지만 while 문 쓰니 out of range 문제 바로 해결!
        if len(people) == 1:
            cnt += 1
            break
        if people[0] + people[-1] <= 100: # 맨앞에거랑 뒤에꺼만 더해서 조건을 만족한다는게 아직 이해가 안가는 부분이긴함.....
            cnt += 1                  # limit 써야지ㅋㅋㅋㅋㅋㅋㅋㅋㅋ 100ㅋㅋㅋㅋㅋ 앞으로 조심합시다!
            people.pop(0)
            people.pop()
        else :
            cnt += 1
            people.pop()
    return cnt
```
하지만 효율성 1문제를 통과를 못했다. 참고 정보 보니, pop(),remove(),del()은 모두 효율성 오류로 처리하는 듯했다.
도대체 저 내장함수 안쓰고도 해결하는 방법이 뭐가 있나 했더니 _cnt += 1 cnt -= 1_ 로 삭제 위치를 조정하고 다녔다. 

```python
def solution(people, limit):
    people.sort()
    length=len(people)
    heavy=length-1
    cnt=0
    light = 0
    while(light<heavy): # 그래도 얘는 이해못하겠다.....
        print(people[light],people[heavy])
        if people[light]+people[heavy]<=limit:
            cnt += 1
            light += 1
            heavy -= 1
        else:
            heavy-=1
    return length-cnt
```

## :mega: 체육복

```python

def solution(n, lost, reserve):
    lst = list(lost) # 이렇게 안했더니 
    for i in lst:
        if i in reserve:
            lost.remove(i)
            reserve.remove(i) 
                              
    lst = list(lost)
    for i in lst:        
        if i-1 in reserve:
            lost.remove(i)
            reserve.remove(i-1)
        elif i+1 in reserve:
            lost.remove(i)
            reserve.remove(i+1)
        
    return n-len(lost)
```
    
    
#### 정리 
-------------
* 중복 요소 고려 안했음. 테스크케이스없었으면 헷갈렸을 법 하지만 그래도 지문에서 잘 찾을 수 있었음
* list끼리 비교할때 중복 요소 제거할때는 for문 말고 set()쓰기
```python
    lst = list(lost)
    lost = set(lost)-set(reserve)   
    reserve = set(reserve)-set(lst)
    lst = list(lost)
```
이렇게도 가능하다. 하지만 out of range 조심하듯 set() 지울때도 지워지는 list와 남는 list 잘 구분해야함.



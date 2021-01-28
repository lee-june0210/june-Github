
# 그리디
> 그리디 알고리즘은 현재 상황에서 가장 좋은 최적의 해만 고르는 방법이다.
즉, 매 순간 제일 최적의 해로 보이는 해를 선택하며 현재의 선택이 나중에 어떠한 영향을 미칠지는 고려하지 않는다. 
따라서 특정 문제를 만났을 때 단순히 현재 상황에서 가장 좋아보이는 최적의 해만 선택해도 문제를 정상적으로 풀어낼 수 있는지 파악해야한다. -> 그리디의 핵심!
정렬을 많이들 한다..
<br>
<br>

## 구명 보트!!!!!!!!!!!!!!!!!!!!!!!!! 정리!!!!!!!!!!!!1111

```python
def solution(people, limit):
    people.sort()
    cnt = 0
    while people : # for문일 땐 out of range 에러를 해결할 수가 없었는데 while 하니깐 해결.
        if len(people) == 1:
            cnt += 1
            break
        if people[0] + people[-1] <= 100: # 맨앞에거랑 뒤에꺼만 더해서 조건을 만족한다는게 아직 이해가...
            cnt += 1               # ㅋㅋㅋ limit 써야지ㅋㅋㅋㅋㅋㅋㅋㅋㅋ 100ㅇㅈㄹ    
            people.pop(0)
            people.pop() # pop(-1)대신 pop()
        else :
            cnt += 1
            people.pop()
    return cnt
```
원래는 2중 for 문을 돌려서 
pop으로 지워가며 list 내용 변화를 시킬때는 for문

```python
def solution(people, limit):
    people.sort()
    length=len(people)
    heavy=length-1
    cnt=0
    light = 0
    while(light<heavy):
        print(people[light],people[heavy])
        if people[light]+people[heavy]<=limit:
            cnt += 1
            light += 1
            heavy -= 1
        else:
            heavy-=1
    return length-cnt
```

## 체육복

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



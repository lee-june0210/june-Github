
# 그리디
> 그리디 알고리즘은 현재 상황에서 가장 좋은 최적의 해만 고르는 방법이다.
즉, 매 순간 제일 최적의 해로 보이는 해를 선택하며 현재의 선택이 나중에 어떠한 영향을 미칠지는 고려하지 않는다. 
따라서 특정 문제를 만났을 때 단순히 현재 상황에서 가장 좋아보이는 최적의 해만 선택해도 문제를 정상적으로 풀어낼 수 있는지 파악해야한다. -> 그리디의 핵심!
정렬을 많이들 한다..
<br>
<br>

## 구명 보트!!!!!!!!!!!!!!!!!!!!!!!!! 정리!!!!!!!!!!!!1111

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



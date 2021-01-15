
# 정렬, 완전 탐색
> 그리디 알고리즘은 현재 상황에서 가장 좋은 최적의 해만 고르는 방법이다.
즉, 매 순간 제일 최적의 해로 보이는 해를 선택하며 현재의 선택이 나중에 어떠한 영향을 미칠지는 고려하지 않는다. 
따라서 특정 문제를 만났을 때 단순히 현재 상황에서 가장 좋아보이는 최적의 해만 선택해도 문제를 정상적으로 풀어낼 수 있는지 파악해야한다. -> 그리디의 핵심!
<br>
<br>

## 체육복

```python
# lost를 기준으로 for문 돌려서 if 조건절 걸어서 앞뒤에 여벌 있으면 빼고 없으면 남겨놓기
# return 값은 n-len(lost)가 어떠하실런지~~~ 

def solution(n, lost, reserve):
    lst = list(lost) # 이렇게 안했더니 
    for i in lst:
        if i in reserve:
            lost.remove(i)
            reserve.remove(i) ## 이 방법 말고 그냥 set()해서 빼버리는 방법도 있었다. 
                              ## 처음에는 for문안에 넣고 if 문 조건 3개를 다 걸었었는데 여벌 체육복이 있는 사람도 도난당하면 자기부터 챙긴다는 설정이 필요했다. 
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
* list끼리 비교할때 중복 요소 제거할때는 for문 말고 set()쓰기
> ex) _a>=b b<brown/2_ 이렇게 했더니 내가 갖고 있는 테케는 다맞아도 문제 풀 때 잡을 수 없는 걸 절대 못잡음 _(a-2)*(b-2) == yellow_ 이런식으로 방정식 세워서 정확한 조건절 구하기
* return 위치
결과값 바로 뜨는 위치가 있다면 return 바로 걸어서 효율성 올리기
* 함수 막 쓰지말기.
함수는 쓰면 확실히 속도가 느려진다. 

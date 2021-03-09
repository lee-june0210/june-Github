# 스택, 큐
----------------
import deque / deq = deque()를 사용하지 않고, stack에서 pop(0)을 사용할 수도 있겠지만 이러면 더 시간복잡도가 

## :mega: 다리를 건너는 트럭
```python
def solution(bridge, weight, truck):
    cnt = 0 
    lst = [bridge] *len(truck) # [bridge]*숫자가 되다니! 참고!
    que = []
    rg = 0
    que_w = 0 # 원래는 아래서 sum()처리했는데 이게 testcase 5 시간초과돼서 이렇게 바꿔봄
    while truck or que : # 이런게 되다니!
        cnt += 1
        for i in range(rg):
            lst[i] -= 1
            if lst[i] == 0:
                que_w -= que[0]
                que.pop(0)
        if truck:
            if que_w + truck[0] <= weight: 원래는 밑에있는 if문하고 and로 엮었었는데 속도도 쫌더 빨라지고 깔끔함
                que.append(truck[0])
                que_w += truck[0]
                truck.pop(0)
                rg += 1
    return cnt
```
다른 사람이 한거 '모의고사'문제랑 같은 충격이다. 이렇게 할 수도 있구나 참고
```python
def solution(bridge_length, weight, truck_weights):
    time = 0
    q = [0] * bridge_length
    
    while q:
        time += 1
        q.pop(0)
        if truck_weights:
            if sum(q) + truck_weights[0] <= weight:
                q.append(truck_weights.pop(0))
            else:
                q.append(0)
    return time
```

#### 참고
-------------
* list 존재여부
while문의 while list:와 같이 if list: 하면 list 존재 여부에 따라 조건절 필터링 

## :mega: 프린터

```python
def solution(p, l):
    cnt = 0
    while p:
        max1 = max(p) # max값이 갱신되는데, while문이 돌때마다 max값을 갱신해준거 좋은 시도.
        if p[0] < max1 : 
            if l == 0:
                l += len(p) # 저번에 구명보트에서 count로 lst안의 값 찾아나갔던 방식, 좋은 시도
            p.append(p[0])
        else :
            cnt += 1
            if l == 0:
                return cnt # retrun은 여기에 한번만 넣어도 성공함
        p.pop(0) # if와 else에 모두 해당돼서 돌아가는 행은 밖으로 빼서 중복을 없애줌
        l -= 1
```

### 정리 
-------------
* enumerate를 사용하지 않고 count 형식으로 location을 쫓아감.
* [1,2,3] 0 3 이라는 반례가 없었으면 해결이 어려웠을 것이다....... but, 반례있으니 금방 찾음! 잘할 수 있음.

#### 참고
-------------
* max() 함수

```python
max1 = max(p)
```
이거면 lst 새로 만들어서 p를 복사한다음에 sort하고 [-1]로 찾아줄 필요가 없음. 저 한줄이면 끝남...


## :mega:주식 가격

```python

answer = []
lst = list(prices)

for i in range(len(lst)):
    cnt = 0
    for j in range(i+1,len(prices)):
        cnt += 1
        if lst[i] <= prices[j]:
            continue
        else:
            break
    answer.append(cnt)
```

### 정리 
-------------
* for문 조건절 사용 가능
```python 
for _ in lst:
    if True:
        continue
    else : 
        break
```
* lst.pop(index) 가능
```python
lst.pop(0)
```
lst.pop()해서 원래 stack 구조처럼 맨 나중에 들어간 것만 나올 수 있다고 생각했는데 index 지정해서 뺄 수 있음

## :mega:기능개발

```python

cnt = 1
lst = [0]*len(progresses)
answer = []
count = 0

while lst:
    for i in range(len(lst)):
        res = progresses[i] + speeds[i]*cnt
        lst[i] = res
        n = len(lst) 
    for _ in range(len(lst)):        
        if lst[0] > 99:
            lst.remove(lst[0])
            progresses.remove(progresses[0])
            speeds.remove(speeds[0])
            count += 1
            
    if len(lst) < n:
        answer.append(count)
        count = 0

    cnt += 1
```

### 정리 
-------------
* remove말고 pop을 사용하면 어떻게 


## :mega:공주 구하기_큐

```python
from collections import deque #######deque 배웠다......

a,k = map(int,input().split())
deq = deque()

for i in range(1,a+1):
    deq.append(i)  
#dq = list(range(1,n+1))
#dp = deque(dp)

ch = 0

while deq:
    res = deq.popleft()
    ch += 1
    if ch != k:
        deq.append(res)
    else:
        ch = 0
print(res)
 ```

### 정리 
-------------
> deque 객체

deque는 스택과 큐를 합친 자료구조이다. 가장자리에 원소를 넣거나 뺄 수 있다.

* 호출 
> from collections import deque 

메서드	설명
deque(iterable, [, maxlen])	초기화 함수이다. iterable(리스트 등)을 인자로 건내면 이를 deque화 시켜준다.
append(x)	x를 덱의 오른쪽에 삽입한다.
popleft()	덱의 가장 왼쪽에 있는 원소를 덱에서 제거하고, 그 값을 리턴한다.
clear()	모든 원소를 지운다.

## :mega:가장 큰수

#### 풀이 방법_3번 풀었는데 풀때마다 헤멤

```python
a, cnt = map(int,input().split())
lst = []
stack = []

while a > 0:
    lst.append(a%10)
    a = a//10
    
lst.reverse()
stack.append(lst[0])    
for i in range(1, len(lst)):
    while len(stack) != 0 and  lst[i] > stack[-1] and cnt > 0: 
        stack.pop()
        cnt -= 1
    stack.append(lst[i])

if cnt != 0:
    stack[:-cnt]

    
print("".join(list(map(str,stack))))
```
2번째 풀었을 때
```python
def solution(number, k):
    lst = list(map(int,list(number)))
    stack = []
    stack.append(lst[0])
    for i in range(1,len(lst)):
        while len(stack) >= 1 and stack[-1] < lst[i] and  k > 0:
            stack.pop()
            k -= 1
        stack.append(lst[i])

    if k == 0:
        return ''.join(map(str,list(stack)))
    else :
        return ''.join(map(str,list(stack[:-k])))
```

### 정리 
------------------
* ''.join()
```python
''.join(list(map(str,stack)))
```
개안외워짐 좀 외워라
list의 ''.join(list_name)을 쓸 때, list의 모든 element들은 문자여야 한다. 즉 list에 저장된 값이 정수이거나 실수이면 이와 같은 에러가 뜰 것이다.
* 숫자, 글자 쪼개기_외우기
```python
lst = list(map(int,list(number)))
```

#### 디버깅
    lst[i] > stack[i-1]
여기서 자꾸 'list out of range' 오류가 떴었음. 글고 오류가 문제가 아니라 i랑 i-1 or i+1 만 비교해서는 답대로 안나오는 알고리즘임.
```
lst[i] > stack[-1]
```
stack[-1]을 통해 문제 해결! pop으로 요소를 제거하는 스택 구조였기에 가능했음. 

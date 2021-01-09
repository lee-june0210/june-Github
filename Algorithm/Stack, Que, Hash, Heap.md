# 스택, 큐, 해시, 힙

## :mega:주식 가격_

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

#### 풀이 방법
    숫자를 다 쪼개서 list에 하나씩 넣기
    자기 앞에가 자기보다 작으면 pop 시키기 ( cnt가 0이 될때까지 )
    자기를 스택에 넣기
    다 돌았는데 cnt가 남으면 [:cnt] 이런거 해서 cnt 나머지 길이만큼 짜르기

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
### 정리 
------------------
> ''.join()

list의 ''.join(list_name)을 쓸 때, list의 모든 element들은 문자여야 한다. 즉 list에 저장된 값이 정수이거나 실수이면 이와 같은 에러가 뜰 것이다.

#### 디버깅
    lst[i] > stack[i-1]
여기서 자꾸 'list out of range' 오류가 떴었음. 답을 살짝 참고해보니 
    lst[i] > stack[-1]
stack[-1]을 통해 문제 해결! pop으로 요소를 제거하는 스택 구조였기에 가능했음. 


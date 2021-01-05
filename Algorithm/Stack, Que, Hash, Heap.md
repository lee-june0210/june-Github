# 스택, 큐, 해시, 힙

## 공주 구하기_큐

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

정리 
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




## 기능개발

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

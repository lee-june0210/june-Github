
# 정렬, 완전 탐색

## 모의고사 

```python
lst1 = [1,2,3,4,5]
lst2 = [2,1,2,3,2,4,2,5]
lst3 = [3,3,1,1,2,2,4,4,5,5]
lst = [0,0,0]
re = []
max = -1

for i in range(len(answer)):
    if answer[i] == lst1[i%len(lst1)]:
        lst[0] += 1
    if answer[i] == lst2[i%len(lst2)]:
        lst[1] += 1
    if answer[i] == lst3[i%len(lst3)]:
        lst[2] += 1


for n,i in enumerate(lst):
    if i >= max:
        max = i
        
for i in range(len(lst)):
    if lst[i] == max:
        re.append(i+1)
 
 ```

### 정리 
-------------
> empty list를 만들어서 for문이 돌때마다 값을 채워 넣는 방식을 알려준 알고리즘


#### 참고
-----------------

```python
for idx, s in enumerate(score):
    if s == max(score):
        result.append(idx+1)
```

max(list)하면 바로 값을 찾아줌. for문 돌려서 max 값을 찾을 필요가 
            






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

### 정리
--------------------
> 새로운 함수 없이 내가 알고 있는 지식으로 풀어냄. 할 수 있다.

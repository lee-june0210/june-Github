
# 정렬, 완전 탐색

## 단어찾기

```python
participant = ["aeo", "kiki", "eden"] 
completion = ["eden", "kiki"]


participant.sort()
completion.sort()

for i in range(len(completion)):
    if participant[i] != completion[i]:
        print(participant[i])
        break
else : 
    print(participant[-1])
```

#### 참고
-------------
> def 함수 속 return

```python
for i in range(len(completion)):
    if participant[i] != completion[i]:
        return participant[i] 
        break
else : 
    return participant[-1] 
```
returnd을 이렇게 바로 뽑아내도됨

## 단어찾기 

```python
n = int(input())
lst = []
nxt_lst = []
for _ in range(n):
    word = input()
    lst.append(word)
for _ in range(n-1):
    nxt = input()
    nxt_lst.append(nxt)
    
lst.sort()
nxt_lst.sort()

list(set(lst) - set(nxt_lst))
```

### 정리 
-------------
> set

* 중복 제거
* [] -> {} 집합으로 형태변환
* set()-set() 빼기 가능; 없는 요소만 남음

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

max(list)하면 바로 값을 찾아줌. for문 돌려서 max 값을 찾을 필요가 없음.
            






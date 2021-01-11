
# 정렬, 완전 탐색
<br>
<br>

## 카펫
```python
def divide(num):
    arr = [] 
    for i in range(3,num//3+1):
        lst = []
        if num%i == 0:
            lst.append(i)
            lst.append(num//i)
            arr.append(lst)
    return arr

def solution(brown, yellow):
    for a,b in divide(brown+yellow):
        print(a,b)
        if (a-2)*(b-2) == yellow :
            return [b,a]
```
....충격의 도가니 원래는 이렇게 했었다. 근데 

```python
def solution(brown, yellow):
    num = brown+yellow
    for i in range(3,num//3+1):
        if num%i == 0:
            if (i-2)*((num//i)-2) == yellow :
                return [num//i,i]
```
이렇게 하니깐 속도가 2배는 빨라졌다........개 충격.................

### 정리 
-------------
* if문 조건은 정확한 방정식으로 하기
> ex) _a>=b b<brown/2_ 이렇게 했더니 내가 갖고 있는 테케는 다맞아도 문제 풀 때 잡을 수 없는 걸 절대 못잡음 _(a-2)*(b-2) == yellow_ 이런식으로 방정식 세워서 정확한 조건절 구하기
* return 위치
결과값 바로 뜨는 위치가 있다면 return 바로 걸어서 효율성 올리기
* 함수 막 쓰지말기.
함수는 쓰면 확실히 속도가 느려진다. 

## 마라톤

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
            






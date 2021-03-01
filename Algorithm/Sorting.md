# 정렬, 완전 탐색
<br>
<br>

## :mega: 문자열 뒤집기 
```python
str1 = list(map(str,input()))
num = len(str1)
lst = []

for i in range(len(str1)):
	lst.append(str1[num-i-1])

str2 = ''.join(map(str,lst))
print(str2)
```
#### 정리 
-------------
* 문제 잘보기
* list(map(str,input())
* lst.append(str1[num-i-1]
* * ''.join(map(str,lst))


## :mega: 요일

```python
a,b = map(int,input().split())

month = [31,59,90,120,151,181,212,243,273,304,334]
day = ["Thr","Fri", "Sat","Sun","Mon","Tue","Wed" ]

if a == 1:
    sum1 = b 
if a > 12 or b >31:
    print("ERROR")
else :
    sum1 = month[a-2]+ b
    num = sum1%7
    print(day[num])
```
2월의 29,30 달과 30일밖에 없는 달은 해결하지 못했다. 
원래는 day부를때랑 month 부를때 def 함수를 만들어서 return값으로 처리했는데, 이렇게 해도 나온다. 최대한 def()함수 사용은 자제하는게 효율성면에서 좋다.

## :mega: 완전수

```python
a,b = map(int,(input().split())) # 구름환경에서는 이렇게 수를 받아서 처리한다. 

lst1 = []
for i in range(a,b+1): # 당연하게 a,b사이일꺼라고 생각했는데...내 착각이었다. 1부터 6일수도 있는거자나  방심하지 않기
	lst = []
	for j in range(1,i):
		if i%j == 0:
			lst.append(j)
	if sum(lst) == i:
		lst1.append(i)
for i in lst1:
	print(i, end=' ') # lst안에 있는 값 꺼내오기......능숙해.......
```
#### 참고
-------------
* join
```
print(' '.join(map(str,lst1)))
```
## :mega: 카펫
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

#### 정리 
-------------
* if문 조건은 정확한 방정식으로 하기
> ex) _a>=b b<brown/2_ 이렇게 했더니 내가 갖고 있는 테케는 다맞아도 문제 풀 때 잡을 수 없는 걸 절대 못잡음 _(a-2)*(b-2) == yellow_ 이런식으로 방정식 세워서 정확한 조건절 구하기
* return 위치
결과값 바로 뜨는 위치가 있다면 return 바로 걸어서 효율성 올리기
* 함수 막 쓰지말기.
함수는 쓰면 확실히 속도가 느려진다. 




## :mega: 단어찾기 

```python
n = int(input())
lst = []
nxt_lst = []
for _ in range(n):
    word = input() # 정해진 수만큼 값 받기
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
* set 기능
1. 중복 제거
2. [] -> {} 집합으로 형태변환
3. set()-set() 빼기 가능; 없는 요소만 남음

### sort() vs sorted() 
-------------
* sort()
사용법 : list.sort()
```python
lst = [1, 3, 2]
print((lst.sort())
# None 
원본 리스트를 정렬하되 반환 값은 None
print(lst)
# [1, 2, 3]
원본 리스트의 순서를 변경
```
* sorted()
사용법 : sorted(list)
```python
lst = [1, 3, 2]
print(sorted(lst))
# [1, 2, 3]
정렬된 새로운 리스틀 반환
print(lst)
원본 리스트에 영향없음
# [1, 3, 2]
```

## :mega: 모의고사 

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

#### 정리 
-------------
> empty list를 만들어서 for문이 돌때마다 값을 채워 넣는 방식을 알려준 알고리즘


#### 참고
-----------------

```python
for s in range(len(score):
    if lst[s] == max(score):
        result.append(idx+1)
```

max(list)하면 바로 값을 찾아줌. for문 돌려서 max 값을 찾을 필요가 없음.
            






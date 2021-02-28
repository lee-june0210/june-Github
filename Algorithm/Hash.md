# 해시

## :mega: 베스트 앨범

```python
def solution(genres, plays):
    answer = []
    def num(n,gen): # 받아야할 값이 너무 많아서 함수를 안으로 넣어봤더니 문제 없었다. answer,
        for i in range(len(plays)):
            if genres[i] == gen and plays[i] == n: # 장르가 같으면서 재생횟수가 같은 고유번호 i를 찾아내는 방법 굿
                if i not in answer:
                    return i
                else:
                    continue # 만약에 재생횟수가 동일하다면 다음껄로 넘어가게 하는 아이디어 굿!
    d = {}
    for i in range(len(genres)): #재생 횟수 합한게 어디가 많은지 볼라고 for문 따로 뺌. 밑에 for문과 합쳐볼라 햇지만 실패
        if genres[i] not in d:
            d[genres[i]] = plays[i]
        else:
            d[genres[i]] += plays[i]
    lst = {}
    for i in range(len(genres)):
        if genres[i] not in lst:
            lst[genres[i]] = []
        lst[genres[i]].append(plays[i])
    while d:
        max1 = [k for k,v in d.items() if max(d.values()) == v] # 알아두면 좋을 거 ㅇㅈ
        i = lst[max1[0]]
        i.sort(reverse=True)
        gen = max1[0]
        answer.append(num(i[0],gen))
        if len(i) != 1:
            answer.append(num(i[1],gen))
        d.pop(max1[0])
    return answer
```
### 정리 
-------------
* for and if in one line
```
for i in v:         # 기존 
    print(i)    
    
[i for i in v]      # 한줄로 했을때
```
```
for i in v:         # 기존
    if i == 12:
        print(i)

[i for i in v if i == 12 ]  # 한줄로 했을 때
```
```
for i in v:         # 기존
    if i == 12:
        print(i)
    else:
        print("No")

[i if i==12 else "No" for i in v] # 한줄로 했을 때
```
* dict
```
d.keys()           // 딕셔너리의 key 조회
d.values()         // 딕너리의 value 조회
d.items()          // 딕셔너리의 key-value를 리스트로 조회
```
* value 값으로 max값 찾기
```
[k for k,v in d.items() if max(d.values()) == v]
```
items(), values() 값을 잘 활용해야함

#### 참고
-------------
* dict 자료 저장 형태
```
d = {}
d["a"] = [1]
d["a"].append(2)
# d = {"a" : [1,2]}
```

## :mega: 전화번호부
```python
def solution(phone_book):

    for i in range (len(phone_book)):
        for j in range (i+1, len(phone_book)):
            if phone_book[j].startswith(phone_book[i]):# startwith의 발견이다....python은 함수빨이군.....
                return False
            elif phone_book[i].startswith(phone_book[j]):
                return False
    return True
```
9일을 고민했던 건데 함수 쓰니깐 22분만에 풀렸다.

#### 정리 
-------------
* startswith 
접두어 일치 찾아주는 함수
_str.startswith('str')_ 하면 일치 여부에 따라 True와 False를 반환한다.

## :mega: 완주하지 못한 선수

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
* def 함수 속 return

```python
for i in range(len(completion)):
    if participant[i] != completion[i]:
        return participant[i] 
        break
else : 
    return participant[-1] 
```
returnd을 이렇게 바로 뽑아내도됨

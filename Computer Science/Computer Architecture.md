# <PART1. 컴퓨터 일반> 
## Computer Architecture


### 기억장치 접근시간


#### 캐시 메모리 참조

<img src = "https://user-images.githubusercontent.com/76678910/107191751-fc125880-6a2f-11eb-9a8d-f3ab5def09da.png" width = "60%" height = "60%"> </img>

CPU는 데이터 처리를 위해 메모리와 끊임없이 데이터를 주고 받는다. 이 때 CPU에 비해 메모리는 속도가 느리기 때문에 메모리에 접근할 때 CPU는 효율적으로 사용되지 못한다.

캐시 메모리는 CPU와 메모리의 속도 차이로 인한 병목 현상을 완화하기 위해 사용한다. 메모리와 CPU 사이에 위치하여 자주 사용하는 데이터를 CPU와 가까운 위치에 저장해 필요할 때마다 빠르게 꺼내쓸 수 있다. CPU가 메모리에 접근하는 횟수를 줄여 성능을 향상

CPU가 메모리에 접근하기 전 먼저 캐시 메모리에서 원하는 데이터의 존재 여부를 확인. 필요한 데이터가 있으면(HIT), 없으면(MISS)

CPU는 캐시 메모리 > 메모리 > 보조기억장치 순으로 접근

* 캐시 적중 : 캐시 메모리 데이터를 CPU 레지스터에 복사

캐시 실패/ 메모리 적중 : 메모리 데이터를 캐시 메모리에 복사, 캐시 메모리의 복제된 내용을 CPU 레지스터에 복사
캐시 실패/ 메모리 실패 : 보조 기억장치에서 필요한 데이터를 메모리에 복사 → 메모리에 복제된 내용을 캐시 메모리에 복제 → 캐시 메모리의 복제된 데이터를 CPU 레지스터에 복제

캐시 메모리 성공 여부는 참조의 지역성 원리에 달려 있다
	# 참조의 지역성 : 짧은 시간 동안 제한된 주소 공간의 일부만 참조되는 경향

#### TLB 메모리 참조

<img src="https://user-images.githubusercontent.com/76678910/107191746-fae12b80-6a2f-11eb-9f51-f65356600457.png" width = "70%" height = "70%"> </img>

TLB 메모리는 일종의 페이지 테이블의 캐시라고 생각

페이지 테이블은 메인 메모리에 저장되기 때문에 프로그램에 의한 모든 메모리 접근은 최소 두 번 필요

실제 주소를 얻기 위한 메모리 주소 접근 한 번과 데이터를 얻기 위한 또 한번의 접근 필요 (CPU로부터 생성된 가상 주소를 메모리에 있는 page table을 통해 실제 주소로 변환) 

먼저 가상 주소를 메모리에 있는 페이지 테이블에 매핑시켜 실제 주소를 알아낸다(만약 테이블의 valid bit가 0이라면 메모리에 페이지가 없으므로 page fault 발생)

알아낸 실제 주소를 사용 캐시로 가서 페이지가 있는지 없는지 비교


<img src="https://user-images.githubusercontent.com/76678910/107191754-fd438580-6a2f-11eb-99d4-24f5cf536a1e.PNG"> </img>

1번 : BEST한 경우. TLB가 hit이므로 페이지 테이블을 볼 필요가 없다. (페이지 테이블을 접근하는 것은 cpu의 가상주소를 실제 주소로 변환하기 위함인데, TLB에 이미 실제 주소가 있기 때문) 즉, 메인 메모리 접근이 필요가 없다. Cache hit이므로 TLB에 의해 가상 주소 → 실제 주소, 이 실제주소를 가지고 cache에 접근해 페이지를 접근한다.

2번 : TLB가 hit이므로 페이지 테이블에 접근하지 않는다. 그러나 cache가 miss이므로 페이지를 읽기 위해 메모리 접근 1회가 필요

3번 : TLB가 miss이므로 페이지 테이블에 접근해 가상 주소 → 실제 주소 변환 작업이 필요(메모리 접근 1회) 만약 페이지 테이블에 접근했는데 valid bit가 0이라면 page fault 발생. Cache는 hit이므로 더 이상의 메모리 접근은 없다

4번 : TLB가 miss이므로 페이지 테이블에 접근. Cache도 miss이므로 메모리에 접근해 페이지를 가져옴. 메모리 접근 2번

5번 : 최악의 경우, 메모리에서 miss가 발생했으므로 page fault가 발생. 즉 가상 페이지의 Valid bit가 0이므로 운영체제가 제어를 넘겨받게 된다. (디스크로부터 페이지를 가져옴 - 시간이 오래걸려 성능이 저하)

6~8번 : 불가능한 경우. 가상 메모리와 캐시 시스템은 계층구조를 이루며 같이 동작. 따라서 데이터가 메인 메모리에 없다면 그 데이터는 캐시에 있을 수 없다.






### 평균 기억장치 접근 시간

* 일반적인 계산법
평균 기억장치의 접근 시간 = 적중률 X 캐시기억장치의 접근 시간 + {(1-적중률) X 주기억장치의 접근 시간}
ex) Tc = 50ns, Tm = 400ns인 시스템에서 캐시 적중률이 70%일 때 평균 기억장치 접근 시간?
0.7 x  50ns + 0.3 x 400ns = 155ns

* TLB 메모리 사용될 경우 계산법
평균 기억장치의 접근 시간 = (TLB 탐색 시간 + 기억장치 접근 시간) X TLB 적중률 + (TLB 탐색 시간 + 2X기억장치 접근 시간) X (1-TLB 적중률)
ex) 페이지 테이블의 TLB 적중률이 80%이고, TLB를 탐색하는 데 20ns, 기억장치에 접근하는 데 100ns가 걸린다면, 실제 기억장치 평균 접근 시간?
		0.8 x 120 + 0.2 x 220 = 140ns


### 기억 장치 용량 계산법

기억장치 용량 = 2(입력 번지선의 수) x (출력 데이터선의 수)
		= 2(워드 수) x 워드 크기
Address Field 크기 = 최대 메모리 용량(2워드 수 x 워드길이)
입력 번지선의 수 = MAR의 크기 = PC의 크기
워드 수 = 2(입력 번지 수)
출력 데이터선의 수 = 워드의 크기 = MBR의 크기 = DR의 크기

ex) 기억용량이 1MByte일 때 필요한 주소선의 개수? 20

2n x 워드 크기 (워드 크기에 대한 언급이 없으면 1Byte로 본다)
1Mbyte = 1024 KByte = 1024 x 1024 Byte = 210 x 210 = 220
20개의 주소선 필요

ex) 입력 번지선이 8개, 출력 데이터선이 8개인 ROM의 기억 용량? 256바이트

28 x 8Bit = 256 x 8Bit = 256 x 1Byte = 256Byte

ex) 기억장치의 총 용량이 4096워드이고, 워드길이가 16Bit일 때 프로그램 카운터(PC), 주소 레지스터(AR), 데이터 레지스터(DR)의 크기는? PC = 8, AR = 8, DR = 16

4096(212) = 2n x 16 이므로 2n = 28
워드수 = 주소선수 = AR = PC 이므로 = 8
워드길이 = DR = 16



### 캐시기억장치

캐시 메모리 쓰기 정책

Write-Through

CPU가 데이터를 사용하면 캐시에 저장되게 되는데, 데이터가 캐시됨과 동시에 주기억장치 또는 디스크로 기입되는 방식을 지원하는 구조의 캐시. 즉, 캐시와 메모리 둘다에 Write하는 방식
장점 : 캐시와 주기억장치에 업데이트를 같이 하여, 데이터 일관성을 유지할 수 있어 안정적
단점 : 속도가 느린 주기억장치 또는 보조기억장치에 데이터를 기록할 때, CPU가 대기하는 시간이 필요하기 때문에 성능이 떨어진다
데이터 로스가 발생하면 안되는 상황에서는 Write Through를 사용하는 것이 좋다

Write-Back

CPU 데이터를 사용할 때 데이터는 먼저 캐시로 기록되는데, 캐시 내에 일시적으로 저장된 후에 블록 단위에 캐시로부터 해제되는 때(캐시안에 있는 내용을 버릴시) 에만 주기억장치 또는 보조기억장치에 기록되는 방식. 즉, 데이터를 쓸 때 메모리에는 쓰지 않고 캐시에만 업데이트를 하다가 필요할 때에만 주기억장치나 보조기억장치에 기록하는 방식
장점 : Write Through보다 훨씬 빠르다, 메모리 접근 횟수가 적다
단점 : 속도가 빠르지만 캐시에 업데이트하고 메모리에는 바로 업데이트 하지 않기 때문에, 캐시와 메모리가 서로 값이 다른 경우가 발생할 때가 있다. 회로가 복잡
빠른 서비스를 요하는 상황에서는 Write Back을 사용하는 것이 좋다

<img scr="https://user-images.githubusercontent.com/76678910/107191743-f9affe80-6a2f-11eb-8b92-a666e9e0b660.PNG"> </img>


개념
쓰기 동작 시 캐시와 주기억장치 동시 쓰기
캐시에만 쓰고 데이터 swap-out시 주기억장치에 복사
장점
구조 단순
캐시, 기억장치 일관성
기억장치 쓰기 동작 횟수 최소화, 시간 단축
단점
버스 트래픽 증가, 쓰기 시간 증가
캐시, 기억장치 일관성 문제

### 메모리 인터리빙

: 메모리 접근 시간을 최소화하기 위해 여러 모듈로 나눈 메모리의 각 모듈에 연속적인 주소를 부여하여  동시 접근하는 기법

목적 

- 버스 경합, 기억장치의 충돌 회피
- 단위 시간당 각 메모리 모듈에 대한 병렬 처리 → 메모리 접근시간 최소화

하위 인터리빙

기억장치 주소가 모듈 단위
하위 비트 : 모듈 선택 신호
상위 비트 : 모듈 내 기억 장소
장점 :다수 모듈 동시 동작 (접근속도 향상)
단점 : 1개 새로운 모듈 추가시, 하드웨어 구조 변경 불가 → 동일수 모듈 추가(확장 한계)
	          한 모듈의 오류가 메모리 전체에 영향을 미침

상위 인터리빙

모듈들에 순차 지정 방식
상위 비트 : 모듈 선택 신호
하위 비트 : 모듈 내 기억 장소
지역성 이용, DRAM 제작에 활용
장점 : 에러 시 한 모듈만 영향
단점 : 같은 모듈 동시접근 어려움

혼합 인터리빙

기억장치 모듈을 뱅크로 그룹화
뱅크 선택 시 상위 인터리빙
뱅크 내 모듈 간 하위 인터리빙
장점 : 상/하위 인터리빙 단점 해결
단점 : 구현 복잡, 어려움

### 10. RAID

: 여러 개의 디스크를 배열하여 속도의 증대, 안정성의 증대, 효율성, 가용성의 증대를 위해 쓰이는 기술

목적

백업이 절대적으로 필요할 때
데이터 손실 없이 여분의 디스크로 용량을 증설할 경우

장점

운용 가용성, 데이터 안정성 증대
디스크 용량 증설의 용이성
디스크 I/O 성능 향상

RAID 0

Concatenate 방식 (두개 이상의 디스크에 데이터를 순차적으로 쓰는 방법)

<img src="https://user-images.githubusercontent.com/76678910/107192196-abe7c600-6a30-11eb-8118-edd0dc089c0b.png"> </img>

장점 : 디스크 기본 공간이 부족할 때 데이터는 보존하며 여분의 디스크를 볼륨에 포함하여 용량 증설이 가능
단점 : 하나의 디스크라도 장애가 발생하면 복구가 어렵고, 패리티(오류검출기능)를 지원하지 않는다

Stripe 방식 (흔히 RAID 0라고 하면 Stripe 방식을 말한다, 두개 이상의 디스크에 데이터를 랜덤하게 쓰는 방법)



장점 : 매우 빠르다, I/O를 담당하는 장치가 별도로 장착된 경우 더 큰 I/O 속도 향상 효과를 볼 수 있음
단점 : Stripe를 구성할 시 기존 데이터는 모두 삭제 되어야 한다.

특징 :

최소 2개의 하드디스크 필요
최대 용량 : 디스크 수 X 디스크 용량
데이터 동시 저장 (공간 효율이 좋음, 속도가 가장 빠르다)
낮은 신뢰성 : 하나의 디스크가 고장 나면 모든 데이터 손실
하드디스크의 용량이 같아야 함 (1TB, 10TB가 있으면 1TB 하드디스크가 용량이 꽉 차면 10TB의 9TB는 사용할 수 없다.
	→ 저장 속도를 높이기 위해 데이터를 나눠서 각 하드에 동시에 저장되도록 설계됨


RAID1

<img src ="https://user-images.githubusercontent.com/76678910/107192194-abe7c600-6a30-11eb-8204-b5f92ddcbf8c.png"></img>

장점 : 디스크 중 하나만 정상이어도 데이터는 보존되어 운영이 가능하기 때문에 가용성이 높고, 복원이 비교적 매우 간단, 읽기 성능이 단일 드라이브에서의 성능과 같거나 훨씬 좋다
단점 : 용량이 절반으로 줄고, 쓰기 속도가 조금 느려짐

특징 :

최소 2개의 하드디스크 필요
최대 용량 : 디스크의 용량
스토리지에 저장되는 모든 데이터는 N개의 물리적인 디스크에 각각 저장되고 모든 데이터는 중복된다.







RAID0+1

<img src="https://user-images.githubusercontent.com/76678910/107192191-aa1e0280-6a30-11eb-9694-224dae12348a.png"></img>

장점 : RAID0의 속도와 RAID1의 안정성이라는 각 장점을 합침, RAID1+0에 비해 기술적으로 단순
단점 : RAID1+0에 비해 확률적으로 안정성이 떨어짐, 복구시간이 오래 걸림

특징 :

최소 4개 하드디스크 필요
최대 용량 : 디스크 수 / (RAID0로 묶는 디스크 개수) X 디스크의 용량
RAID0로 먼저 묶고, 그 다음 RAID1로 묶는 방법, 디스크 N개를 A개씩 RAID0로 묶고, RAID0로 스트라이핑 된 볼륨 N/A개를 RAID1로 미러링

RAID1+0


#### CISC, RICS

CISC

특징

연산에 처리되는 복잡한 명령어들을 수백 개 이상 탑재하고 있는 프로세서
명령어가 복잡하기 때문에 명령어를 해석하는 데 시간이 오래 걸리며, 명령어 해석에 필요한 회로도 복잡하다. → 병렬처리 불가능
복잡한 명령 → 발열이 날 수 있음 → 핸드폰에 사용 불가
복잡한 명령 → 가변길이 명령어 형식 사용 → 파이프라인 기법 사용 불가
설계가 복잡하지만 복합적인 명령으로 인해, 프로그래밍 작업이 간단해짐
다양한 주소지정 모드를 사용
RISC 프로세서에 비해 전력 소모가 많으며 처리 속도가 느림
다양한 명령어로 메모리에 접근
마이크로 프로그래밍 제어방식
가격 비쌈
전력소모 크다
완벽한 하위 호환성
하나의 프로세서가 일련의 명령어를 순차적으로 처리하기 좋음
ex) 인텔의 x86 계열, 모토로라의 M68000, AMD의 인텔 호환 CPU, 386, 486, 펜티엄

RISC

특징

컴퓨터의 실행 속도를 높이기 위해 복잡한 처리를 소프트웨어에 맡기고, 명령 세트를 축소한 컴퓨터
복잡한 80% 명령어를 제거하여 사용빈도가 높은 명령어 위주로 20%의 명령어를 H/W화하여 처리속도를 향상시킨 프로세서
명령의 대부분은 1머신 사이클에서 실행된다
명령어 길이가 고정적 → 해석 속도 빠름 → 병렬 처리 가능 → 파이프라인 가능
CISC에 비해 상대적으로 많은 범용 레지스터 사용 → 주기억장치에서 레지스터로 가져와서 처리 → 빠르다
메모리 참조는 LOAD와 STORE만으로 가능 → 복잡한 어드레싱 모드를 피함
프로그램 구조가 복잡, 하드웨어는 간단
고정 배선 제어로 마이크로 프로그래밍 방식보다 빠르다
속도가 빠른 그래픽 응용 분야에 적합, 워크스테이션에 주로 사용
분기 위치가 정해져 있고 비순차 처리도 가능
처리 비트 단위가 변하거나 CPU의 구조가 조금만 바뀌어도 하위 프로세서와의 호환성이 떨어져 문제가 발생
ex) ARM, 애플 PowerPC, SUN 사의 SPARC, 워크스테이션, 매킨토시

 		
<img src ="https://user-images.githubusercontent.com/76678910/107192807-72fc2100-6a31-11eb-9453-ac71275a7711.PNG"></img>
 

CRISC

CISC방식은 RISC CPU에 비해 탑재된 트랜지스터가 수배 이상 많아짐
트랜지스터 수가 많아지면 그만큼 높은 집적도 기술이 필요
성능 향상에도 여러 제약이 따름
최근에는 CISC와 RISC를 혼합하여 제품을 출시하는 추세

[개인용 컴퓨터와 같이 호환성이 절대적으로 필요한 PC 환경에서는 당분간 CISC 강세]
[좀 더 전문적인 용도에서는 효율적이고 빠른 성능의 RISC가 우위]





### 1.1. 논리 회로

* 기본 게이트
<img src="https://user-images.githubusercontent.com/76678910/104309610-c7d17800-5515-11eb-8d64-11100e2ca46d.jpg" width="50%" height="50%" title="px(픽셀) 크기 설정" alt="RubberDuck"></img>


조합 논리 회로

반가산기 : 1bit짜리 2진수 2개를 덧셈한 합(S)와 자리올림수(C)를 구하는 조합논리회로
       	
반감산기 : 1bit짜리 2진수 2개를 뺄셈한 차(D)와 빌려오는 수(B)를 구하는 조합논리회로
    	

전가산기 : 뒷자리에서 올라온 자리올림수(Ci)를 포함하여 1bit 크기의 2진수 3자리를   더하여 합(Si)과 자리올림수(Ci+1)을 구하는 조합논리회로
           
        
 
전감산기 : 입력 변수 3자리의 뺄셈에서 차(D)와 빌려오는 수(B)를 구하는 조합논리회로
          
    

디코더 : n Bit의 code화된 정보를 그 code의 각 bit 조합에 따라 2n개의 출력으로 번역하는 회로
          
          
인코더 : 2n개의 입력선 중에서 하나가 선택되면 그에 따른 n개의 출력선으로 2진 정보가 출력되는 회로
           

멀티플렉서 : 2n개의 입력선 중 1개를 선택하여 그 선으로부터 입력되는 값을 1개의 출력선으로 출력시키는 회로
2n개의 입력선 중 1개의 선을 선택하기 위해 n개의 선택선을 이용
 

응용

	●  반가산기를 이용해 전가산기를 구현하라.
              

  

● 3X8 디코더로 전가산기를 구현하라







● 3X8 디코더로 전감산기를 구현하라


2. 보수

고정소수점의 음수 표현 방법 - 2진 연산

종류
부호화 절대치
1의 보수
2의 보수
범위(n 비트)
-(2n-1 - 1)~2n-1-1
-(2n-1 - 1)~2n-1-1
-(2n-1)~2n-1-1
0의 표현(8비트)
+0 : 0000 0000
- 0 : 1000 0000
→ 0이 2가지 존재(+0, -0)
+0 : 0000 0000
- 0 : 1111 1111
→ 0이 2가지 존재(+0, -0)
+0 : 0000 0000
→ 0이 2가지 존재(+0)
(-0은 성립이 안됨 : 
1의 보수 끝에
1을 더하면 1이 나온다)
n = 8
-127~127
-127~127
-128~127


① 부호화 절대치
+25와 -25를 2진 연산으로 표현하시오(1Byte)

종류
-25
+25
부호화 절대치법
양수 25를 8Bit 2진수로 표현한 후 부호 비트만 1로 바꾸어 준다.
00011001 → 10011001
●양수는 표현 방식이 모두 같음

●양수 25를 2진수로 변경한 후 0을 추가하여 8Bit로 자리를 맞춘다.
11001 → 00011001
부호화 1의 보수법
양수 25를 8Bit 2진수로 표현한 후 1의 보수를 구한다.
00011001 → 11100110
부호화 2의 보수법
양수 25를 8Bit 2진수로 표현한 후 2의 보수를 구한다.
00011001 → 11100111
      2) 고정소수점의 음수 표현 방법 - 10진 연산

* 언팩 연산

하나의 바이트에 한 개의 숫자를 표시하는 방식
4개의 존 비트와 4개의 숫자 비트를 사용
연산이 불가능, 데이터의 입 출력에 사용
최하위(가장 오른쪽) 바이트의 존 부분을 부호로 사용
Zone 부분 : 무조건 1111 = F16 을 넣는다
Digit 부분 : 10진수 1자리를 4Bit 2진수로 표현
Sign 부분 : 양수는 1100 = C16, 음수는 1101 = D16, 부호 없는 양수는 1111 = F16 


Zone
Digit
Zone
Digit
Zone
Digit
…
Sign
Digit
<------   1Byte ------->


② 팩 연산

하나의 바이트에 BCD 코드 두 개의 숫자를 표시하는 방식
연산이 가능, 데이터의 입 출력이 불가능
최하위(가장 오른쪽) 바이트의 4Bit 부분을 부호로 사용
Digit 와 Sign으로 구성
Digit 부분 : 10진수 1자리를 4Bit 2진수로 표현
Sign 부분 : 양수는 1100 = C16, 음수는 1101 = D16, 부호 없는 양수는 1111 = F16 

Digit
Digit
Digit
Digit
Digit
Digit
...
Digit
Sign


3. 비트연산

BCD 코드
	
10진수 1자리의 수를 2진수 4Bit로 표현
8421 코드라고도 함
가중치 코드
ex) 10진수 125를 BCD코드로 표현 → 0001 0010 0101

Excess-3 코드(3 초과 코드)

BCD 코드에 3을 더하여 만든 코드
모든 비트가 동시에 0이 되는 경우는 없다
자기 보수 코드, 비가중치 코드
Gray 코드

BCD 코드의 인접하는 비트를 X-OR 연산하여 만든 코드
1Bit만 변화시켜 다음 수치로 증가시키기 때문에 하드웨어적인 오류가 적다
아날로그 정보를 디지털 정보로 변환하는 데 사용

2진수를 Gray Code로 변환하는 방법	

첫 번째 그레이 비트는 2진수 비트를 그대로 내려쓴다
두 번째 그레이 비트부터는 변경할 2진수의 해당 번째 비트와 그 왼쪽의 비트를 XOR 연산하여 씀
ex) 2진수 1001을 Gray Code로 변환하시오.



Gray Code를 2진수로 변환하는 방법

첫 번째 2진수 비트는 그레이 비트를 그대로 내려쓴다
두 번째 2진수 비트부터는 왼쪽에 구해 놓은 2진수 비트와 변경할 그레이 코드의 해당 번째 비트를 XOR 연산하여 씀
ex) Gray Code 1101을 2진수로 변환하시오


패리티 검사 코드

전송된 코드의 오류를 검사하기 위해 데이터 비트 외에 1Bit의 패리티 체크 비트를 추가하는 것으로 1Bit의 오류만 검출할 수 있다
오류를 검출할 수는 있지만 오류를 수정할 수는 없다
짝수 개의 오류가 발생했을 시 검출해 낼 수 없다
오류를 발견해도 어디에 오류가 있는지 모른다




Odd Parity

코드에서 1인 비트의 수가 홀수가 되도록 0이나 1을 추가
ex) 101000010에 홀수 패리티를 추가하시오
		10100001 → 101000010 (1의 개수가 홀수이므로 0을 추가)

Even Parity

코드에서 1인 비트의 수가 짝수가 되도록 0이나 1을 추가
ex) 10100001에 짝수 패리티를 추가하시오
		10100001 → 101000011 (1의 개수가 홀수이므로 1을 추가)

해밍 코드

오류를 스스로 검출하여 교정이 가능한 코드
2Bit의 오류 검출 가능, 1Bit의 오류 교정 가능
2개 이상의 오류는 검출 불가능
데이터 비트 외에 오류 검출 및 교정을 위한 잉여 비트가 많이 필요
해밍 코드 중 1,2,4,8,... 2n번째는 오류 검출을 위한 패리티 비트

ex) BCD 코드 1011에 대한 해밍 코드를 구하시오 (짝수 패리티 이용)

4비트 이므로 패리티 비트가 들어갈 자리인 1,2,4번 째 자리를 비운 나머지 자리에 4비트를 적는다

1
2
3
4
5
6
7
H
H
1
H
0
1
1

1번 비트는 3, 5, 7번 비트를 이용하여 1인 비트의 수가 짝수가 되도록 한다                   (n번 패리티 비트를 결정하기 위해서는 n번 비트에서 시작하여 n비트를 포함하고 n비트씩 건너뛴 비트가 대상이 된다)

1
2
3
4
5
6
7
0
H
1
H
0
1
1

2번 비트는 3, 6, 7번 비트를 이용하여 1인 비트의 수가 짝수가 되도록 한다

1
2
3
4
5
6
7
0
1
1
H
0
1
1

4번 비트는 5, 6, 7번 비트를 이용하여 1인 비트의 수가 짝수가 되도록 한다

1
2
3
4
5
6
7
0
1
1
0
0
1
1


1001100을 수신해야 하는데 1011100을 수신했을 때 오류 교정 (짝수 패리티)

1,3,5,7에 있는 1의 개수가 짝수가 아님 (P1 = 1)
1
2
3
4
5
6
7
1
0
1
1
1
0
0

2,3,6,7에 있는 1의 개수가 짝수가 아님 (P2 = 1)
1
2
3
4
5
6
7
1
0
1
1
1
0
0

4,5,6,7에 있는 1의 개수가 짝수 (P3 = 0)
1
2
3
4
5
6
7
1
0
1
1
1
0
0

P3 P2 P1 (※순서 지킬 것) = 011(2) → 3번째 비트를 수정

1
2
3
4
5
6
7
1
0
0
1
1
0
0


체크섬

네트워크를 통해서 전송된 데이터의 값이 변경되었는지 무결성을 검사하는 값
네트워크를 통해서 수신된 데이터에 오류가 없는지 여부를 확인

송신부
모든 Byte 데이터를 더함
발생하는 캐리는 더해주기
캐리니블(최상위 니블, 가장 앞에 위치한 4bit를 가리키는 컴퓨터 용어) 버림
1의 보수를 취해 체크섬을 만듬
수신부
모든 Byte 데이터 + 체크섬
캐리니블 버림
0x00이 나오면 오류가 발생하지 않은 것으로 판단(오류가 발생해도 나오는 예외가 있음)
0x00이 나오지 않으면 오류가 발생한 것으로 판단

ex) IP 헤더 체크섬 예시 
4500 003c 1c46 4000 4006 b1e6 ac10 0a63 ac10 0a0c

다 더하면 2 4e17 → carry 더함 → 4e19
0100 1110 0001 1001 (맨 앞 캐리니블 버림)
1110 0001 1001 (1의 보수 처리)
0001 1110 0110 (헤더 체크섬)

오류 판단
모든 Byte 데이터 + 체크섬 = 0x4e19 + 0x1e6 = 0x4fff
캐리니블 버림 = 1111 1111 1111
0xfff가 나왔기 때문에 오류가 발생했음을 알 수 있음

4. 자료의 외부적 표현 종류

BCD 코드

6비트로 구성, 26 = 64가지 문자 표현 가능
왼쪽 2비트는 존 비트, 나머지 4비트는 디지트 비트로 구성
숫자를 표현할 경우 4비트가 필요, 문자를 표현할 때는 6비트 필요

ASCII 코드

미국 정보 교환 표준 코드로 데이터 통신 및 마이크로컴퓨터에서 주로 사용
7비트로 구성, 27 = 128가지 문자 표현 가능 (0x00 ~ 0x7F)
영문 키보드로 입력할 수 있는 모든 기호들이 할당되어 있는 부호 체계
매우 단순하고 간단하여 어느 시스템에서도 적용가능
2바이트 이상의 코드를 표현할 수 없다
왼쪽 3비트는 존 비트, 나머지 4비트는 디지트 비트로 구성
패리티 비트를 포함하여 8비트로 사용하기도 함

UniCode

전 세계의 모든 문자를 컴퓨터에서 통일된 방법으로 표현하고 사용할 수 있도록 설계된 코드, 산업계에서 사용하는 표준 코드
다국어 환경에서 서로 호환되지 않는 문제점을 해결하기 위해 현존하는 문자 인코딩 기법들을 유니 코드로 교체하는 것이 목적
2바이트 코드로 65,536개의 문자 표현 가능
UTF-8 유니 코드는 영문, 숫자, 기호는 1바이트, 한글과 한자 등은 3바이트로 표현
인코딩 종류에 따라 멀티바이트 공간이 달라지는데, 언어에 적합하지 않는 인코딩을 사용하면 공간이 낭비될 수 있다 (ex 영어에 UTF-32를 사용하는 경우)

EBCDIC 코드

주로 범용 컴퓨터에서 정보 처리 부호로 사용, 확장 이진화 10진 코드라고도 한다
8비트로 구성되며 28 = 256가지 문자 표현 가능
왼쪽 4비트는 존 비트, 나머지 4비트는 디지트 비트로 구성
중 대형급 이상의 컴퓨터에서 사용하는 코드 기법으로 알파벳 문자 코드가 연속적으로 정의되지 못한다


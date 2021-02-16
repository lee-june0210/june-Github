#### 빅데이터 
한대의 컴퓨터로는 저장하거나 연산하기 어려운 규모의 거대 데이터

#### 분산
여러대의 컴퓨터로 나눠서 일을 처리함

#### 저장
데이터를 저장함.

#### 분석
데이터가 저장된 컴퓨터에서 데이터를 분석하고 그 결과를 합친다.


### 용어 정리
----------------------
* 넷캣(Netcat)

TCP나 UDP 프로토콜을 사용하는 네트워크 연결에서 데이터를 읽고 쓰는 간단한 유틸리티 프로그램이다. 일반적으로는 UNIX의 cat과 비슷한 사용법을 가지고 있지만 cat이 파일에 쓰거나 읽듯이 nc는 network connection에 읽거나 쓴다. 이것은 스크립트와 병용하여 network에 대한 debugging, testing tool로써 매우 편리하지만 반면 해킹에도 이용범위가 넓다.

* 아파치 하이브(Apache Hive)

하둡에서 동작하는 데이터 웨어하우스(Data Warehouse) 인프라 구조로서 데이터 요약, 질의 및 분석 기능을 제공한다.

* compresstion
압축

* RDD(Resilient Distributed Data)
RDD는 스파크에서 기본적인 데이터 단위라고 볼 수 있다.
  - Resilient : Memory 내 데이터 손실 시, 다시 생성할 수 있음. 즉, 유실된 파티션을 재연산해 복구(탄력적)
  - Distributed : Cluster를 통해 메모리에 분산되어 저장(분산)
  - Dataset : 파일을 통해 가져올수있음 

#### RDD 함수	설명
-------------

* map(func)	_func_로 처리된 새로운 데이터셋 반환
* filter(func)	_func_에서 true를 반환한 값으로 필터링
* flatMap(func)	_func_는 배열(혹은 Seq)을 반환하고, 이 배열들을 하나의 배열로 반환
* distinct([numPartitions])	데이터셋의 중복을 제거
* groupByKey([numPartitions])	키를 기준으로 그룹핑 처리. (K, V) 쌍을 처리하여 (K, Iterable)로 반환
* reduceByKey(func, [numPartitions])	키를 기준으로 주어진 _func_로 처리된 작업 결과를 (K, V)로 반환
* sortByKey([ascending], [numPartitions])	키를 기준으로 정렬
* reduce(func)	_func_를 이용하여 데이터를 집계(두 개의 인수를 받아서 하나를 반환). 병렬처리가 가능해야 함
* collect()	처리 결과를 배열로 반환. 필터링 등 작은 데이터 집합을 반환하는데 유용
* count()	데이터셋의 개수 반환
* first()	데이터셋의 첫번째 아이템 반환(take(1)과 유사)
* take(n)	데이터셋의 첫번째 부터 _n_개의 배열을 반환
* saveAsTextFile(path)	데이터셋을 텍스트 파일로 지정한 위치에 저장
* countByKey()	키를 기준으로 카운트 반환
* foreach(func)	데이터셋의 각 엘리먼트를 _func_로 처리. 보통 Accmulator와 함께 사용
* sc.parallelize() 파이썬 리스트를 스파크 클러스터로 가져오는 함수



출처: https://devanix.tistory.com/307 [┗System∑Sec†ion┛]

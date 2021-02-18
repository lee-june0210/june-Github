
<img src = "https://user-images.githubusercontent.com/76678910/108342830-963b8300-721e-11eb-9622-b6a4c72708a3.png"></img>

#### 유형 정리 

* DB를 불러오기 -> Please accomplish following activities.
  - sqoop으로 부르는 경우
  - mysql로 부르는 경우
* code snippet과 output 주고 만들라고 하기
* hive 어쩌구 
* csv 파일 제공

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

* 스쿱(sqoop)

관계형 데이터베이스와 하둡 사이에서 데이터 이관을 지원하는 툴이다. 스쿱을 이용하면 관계형 데이터베이스의 데이터를 HDFS, 하이브, Hbase에 임포트(import)하거나, 반대로 관계형 DB로 익스포트(export)할 수 있다. 

* ORC(Optimized Row Columnar)

칼럼 기반의 파일 저장방식으로, Hadoop, Hive, Pig, Spark등에 적용가능합니다. 데이터베이스의 데이터를 읽을 때 보통 칼럼단위의 데이터를 이용하는 경우가 많습니다. ORC는 칼럼단위로 데이터를 저장하기 때문에 칼럼의 데이터를 찾는 것이 빠르고, 압축효율이 좋습니다.

* Parquet
컬럼 기준 저장 포맷으로 파일크기, 쿼리 성능 모두 효율성을 가진다.

파일크기: 동일한 컬럼을 나란히 모아 저장하기 때문에 인코딩 효율이 높음
쿼리성능: 쿼리에 필요하지 않는 컬럼은 처리하지 않기 때문에 효율이 높음
용어

* case class

클래스와 유사하지만 약간의 차이가 존재합니다. 기본적으로 불변이며 불변 데이터를 모델링하기에 좋습니다.
* Hue(Hadoop User Experience

Apache Hadoop 클러스터와 함께 사용되는 웹 기반 사용자 인터페이스입니다. Hue는 다른 Hadoop 에코시스템과 함께 그룹화되어 Hive 작업 및 Spark Job 등을 실행할 수 있습니다.

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
* sc.parallelize() 파이썬 리스트를 스파크 클러스터로 가져오는 함수
* sc.textFile() csv도 얘로 부를수있나봐



#### 출처
----------------------------
https://devanix.tistory.com/307 [┗System∑Sec†ion┛] <br>
https://excelsior-cjh.tistory.com/56 [EXCELSIOR]

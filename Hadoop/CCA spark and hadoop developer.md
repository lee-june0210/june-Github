# CCA Spark and Hadoop Developer (CCA175)
------------------------------
Apache Hadoop은 상용 하드웨어로 구축 된 컴퓨터 클러스터에서 대용량 데이터 세트의 분산 스토리지 및 분산 처리를위한 오픈 소스 소프트웨어 프레임 워크입니다.<br>
Hadoop의 모든 모듈은 하드웨어 오류가 일반적이며 프레임 워크에 의해 자동으로 처리되어야한다는 기본적인 가정하에 설계되었습니다. <br>
Apache Hadoop의 핵심은 HDFS로 알려진 스토리지 부분과 MapReduce라는 처리 부분으로 구성됩니다.<br>
Hadoop은 파일을 큰 블록으로 분할하고 클러스터의 노드에 배포합니다.

### Spark란?

빅데이터 분산 처리 시스템 / 빅데이터 클러스터 환경에서 데이터를 병렬 처리 할 수 있는 오픈소스 소프트웨어  
기존 Disk 기반으로 처리되는 MapReduce의 처리 한계를 극복하고자 연구하여 개발




<img src = "https://user-images.githubusercontent.com/76678910/108342830-963b8300-721e-11eb-9622-b6a4c72708a3.png"></img>

* 

### hadoop environment
#### CDP Private Cloud Installation

Creating a CDP Private Cloud Base cluster requires multiple, Internet-connected Linux machines.

You must be able to log in to the Cloudera Manager Server host using the root user account or an account that has passwordless sudo privileges.
The Cloudera Manager Server host must have uniform SSH access on the same port to all hosts. For more information, see Runtime and Cloudera Manager Networking and Security Requirements.
SELinux must be disabled or set to permissive mode before running the installer.



> 210222 

0. 박성면이 즐겨찾기 해놓은 사이트 가서 사태의 심각성 파악
1. cloudera 제공 CDP private cloud 설치 작업 시작
2. linux 환경 제공 요구해서 ubuntu 설치
3. SELinux 해제 작업 중 박성면한테 2시에 전화옴 hadoop 작업 중단
4. java,python 확인
5. spark 다운로드, 7 zip file manager로 압축해제
6. progra~2로 공백 오류 제거
7. 아직도 오류뜨길래 

9. java는 예상하지 못했습니다 .오류 해결했더니 이제는 exception in thread "main" java.lang.verifyerror 머시기 scala 문젠줄 알고 scala 설치
10. 이와중에 갑자기 scala 폴더 접근 불가 선언
11.  jdk버전 문제인것같음. 
12. spark 버전을 2.4로 다시깜 

#### 유형 정리 

* DB 생성(mysql, hive) 후, import or export로 값 넣고 데이터 전처리 조회하기
  - sqoop으로 부르는 경우
  - mysql로 부르는 경우
* 데이터 제공
  - output 주고 필요한 코드 요구하는 경우
  - sum 등 뽑아내라고 요구하는 경우
  - local에 저장(csv,json), python으로 불러내서 전처리 한다음 요구 사항 파일 형식에 맞춰 다시 저장
* 파일 제공(csv, txt) 후 요구 수행
  - filter 등 처리하고 다시 저장하기
  - 안에 있는 데이터들로 작업하기(단어 빈도수)
  - import or export
* python 활용
* hive 어쩌구 
* 제공한 것들로 log를 멈추라는디 
* XXX,YYY

import org.apache.spark.sql._
import org.apache.spark.sql.SaveMode
val sqlContext = new org.apache.spark.sql.SQLContext(sc)
val df = sqlContext.read.format("com.databricks.spark.csv").load("work/EmployeeName.csv")
df.show
뭐지........뭐가 먹힌거지........

#### mysql 오류
http://blog.naver.com/PostView.nhn?blogId=islove8587&logNo=221970366883
mysqld.sock 파일은 mysql 서버가 시작함과 동시에 생성되며, 꺼지면 mysqld 디렉터리 째로 없어진다.

#### Read a file from HDFS using Spark

First open core-site.xml file from location $HADOOP_HOME/etc/hadoop and check the value of property fs.defaultFS. Let's say the value is hdfs://localhost:9000 and the file location in hdfs is /home/usr/abc/fileName.txt. Then, the file URL will be : hdfs://localhost:9000/home/usr/abc/fileName.txt and following command used to read file from hdfs:

var result= scontext.textFile("hdfs://localhost:9000/home/usr/abc/fileName.txt", 2)

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

### RDD 함수설명
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
* join() 두 개의 키-값 RDD를 사용하여 내부 조인을 수행합니다. 이 작업을 수행하려면 키가 일반적으로 비슷해야합니다.
* keyBy()  각 데이터 항목에 함수를 적용하여 두 구성 요소 튜플 (키-값 쌍)을 구성합니다. 함수의 결과는 키가되고 원래 데이터가 값이됩니다.
* subtractByKey() key 값이 첫번째 RDD에서 항목을 제거하기위한 기준으로 자동으로 사용됩니다.
* union()
* intersection()
* a
scala> rdd1.union(rdd2).collect()

res11: Array[String] = Array(Spark, Scala, Akka, Scala)


교집합.
scala> rdd1.intersection(rdd2).collect()


차집합(A-B)

scala> rdd1.subtract(rdd2).collect()
res14: Array[String] = Array(Spark)
scala> val hash1 = sc.parallelize( Seq(("1", "A"), ("2", "B"), ("3", "C"), ("1","D")))
hash1: org.apache.spark.rdd.RDD[(String, String)] = ParallelCollectionRDD[64] at parallelize at <console>:24



scala> val hash2 = sc.parallelize( Seq(("1", "W"), ("2", "X"), ("3", "Y"), ("2","Z")))
hash2: org.apache.spark.rdd.RDD[(String, String)] = ParallelCollectionRDD[65] at parallelize at <console>:24





scala> hash1.join(hash2).collect()
res15: Array[(String, (String, String))] = Array((1,(A,W)), (1,(D,W)), (2,(B,X)), (2,(B,Z)), (3,(C,Y)))


cogroup 함수는 (K, V)를 (K, Iterable<V>)로 변환한다.


scala> hash1.cogroup(hash2).collect()
res16: Array[(String, (Iterable[String], Iterable[String]))] = Array((1,(CompactBuffer(A, D),CompactBuffer(W))), (2,(CompactBuffer(B),CompactBuffer(X, Z))), (3,(CompactBuffer(C),CompactBuffer(Y))))



### HDFS 명령어 정리
-------------
1) appendToFile

Local 파일들을 hdfs에 append 저장하기 위한 목적
Usage: hdfs dfs -appendToFile {localsrc} ... {dst}

2) cat

해당 파일을 stdout으로 찍어서 보여준다. (linux 명령어 cat과 동일)
Usage: hdfs dfs -cat URI [URI ...]

3) chgrp

해당 파일의 오너이거나 슈퍼오너라면, 해당 파일의 그룹 권한을 변경가능하다.
Usage: hdfs dfs -chgrp [-R] GROUP URI [URI ...]

4) chmod

해당 파일의 오너이거나 슈퍼오너라면, 특정 파일의 permission 수정. -R 옵션과 함께라면 예하 파일들에 대해서 동일하게 permission 적용 가능
Usage: hdfs dfs -chmod [-R] {MODE[,MODE]... | OCTALMODE} URI [URI ...]

5) chown

슈퍼오너일 경우 해당 파일의 owner를 변경. 상세 Permission guide(바로가기) 참고
Usage: hdfs dfs -chown [-R] [OWNER][:[GROUP]] URI [URI ]

6) copyFromLocal

Local 파일을 hdfs에 업로드. put명령어와 유사
Usage: hdfs dfs -copyFromLocal {localsrc} URI

7) copyToLocal

Hdfs에 있는 파일을 local directory에 다운로드, get 명령어와 유사
Usage: hdfs dfs -copyToLocal [-ignorecrc] [-crc] URI {localdst}

8) count

Directory 개수, file 개수 등을 카운트하여 숫자로 보여줌. 
Usage: hdfs dfs -count [-q] [-h] 
-count : DIR_COUNT, FILE_COUNT, CONTENT_SIZE FILE_NAME 을 보여줌
-count -q : QUOTA, REMAINING_QUATA, SPACE_QUOTA, REMAINING_SPACE_QUOTA, DIR_COUNT, FILE_COUNT, CONTENT_SIZE, FILE_NAME 을 보여줌
-h : Show sizes human readable format 

9) cp

Hdfs내부에서 파일을 복붙함. 만약 복사하고자 하는 대상이 여러개라면 붙여넣는 곳은 반드시 Directory여야 한다.
Usage: hdfs dfs -cp [-f] [-p | -p[topax]] URI [URI ...] {dest}
-f : Overwrite the destination if it already exist
-p : 파일 속성(timestamps, ownership, permission, ACL, XAttr)을 유지하고 복붙 수행

10) du

Hdfs내부의 특정 file이나 directory의 size를 보여줌
Usage: hdfs dfs -du [-s] [-h] URI [URI ...]
-s : 각각의 파일(혹은 directory) size의 sum 값을 보여줌
-h : Show human-readable format

11) dus

특정 file의 length를 보여줌.
Usage: hdfs dfs -dus {args}
 
12) expunge

휴지통 비우기(완전 삭제)
Usage: hdfs dfs -expunge
 
13) get

Hdfs의 파일을 local directory로 다운로드
Usage: hdfs dfs -get [-ignorecrc] [-crc] {src} {localdst}

14) getfacl

Hdfs의 특정 파일 혹은 디렉토리의 ACLs(Access Control Lists)정보를 보여줌
Usage: hdfs dfs -getfacl [-R] {path}
 
15) getfattr

Hdfs의 특정 파일 혹은 디렉토리의 속성 정보들을 나열, 보여줌
Usage: hdfs dfs -getfattr [-R] -n name | -d [-e en] {path}
-R : 파일 혹은 디렉토리 이하의 폴더들에 대한 정보 보여줌

16) getmerge

Hdfs내부의 source file을 local file에 append하여 붙여 다운로드
Usage: hdfs dfs -getmerge {src} {localdst} [addnl]

17) ls

특정 디렉토리의 파일 혹은 디렉토리를 보여줌
Usage: hdfs dfs -ls [-R] {args}
-R : 특정 디렉토리 이하에 대해서 정보를 보여줌

18) lsr

ls -R 과 동일하게 작동
Usage: hdfs dfs -lsr {args}
 
19) mkdir

특정 path에 directory 생성
Usage: hdfs dfs -mkdir [-p] {paths}

20) movefromLocal

Local의 파일을 hdfs에 저장. put과 비슷하지만 저장 이후 local file은 삭제
Usage: hdfs dfs -moveFromLocal {localsrc} {dst} 

21) moveToLocal

Hdfs의 파일을 local에 저장. get과 비슷하지만 저장 이후 hdfs file은 삭제
Usage: hdfs dfs -moveToLocal [-crc] {src} {dst}

22) mv

Hdfs내부에서 파일을 옮김
Usage: hdfs dfs -mv URI [URI ...] {dest}

23) put : Local의 파일들을 hdfs에 저장
Usage: hdfs dfs -put {localsrc} ... {dst}

24) rm

Hdfs의 특정 폴더 혹은 파일을 삭제
Usage: hdfs dfs -rm [-f] [-r|-R] [-skipTrash] URI [URI ...]
-R : 특정 디렉토리 이하의 폴더 모두 제거
-r : -R과 동일
-skipTrash : 즉시 완전 삭제

 
25) rmr

rm -r과 동일한 명령어
Usage: hdfs dfs -rmr [-skipTrash] URI [URI ...]

26) setfacl

Hdfs의 특정 폴더 혹은 파일에 대해 Access Control Lists(ACLs)를 set
Usage: hdfs dfs -setfacl [-R] [-b|-k -m|-x {acl_spec} {path}]|[--set {acl_spec} {path}]

27) setfattr

Hdfs의 특정 폴더 혹은 파일에 대해 속성을 set
Usage: hdfs dfs -setfattr -n name [-v value] | -x name {path}
 
30) tail : 특정 file에 대해 마지막 kilobyte을 stdout으로 보여줌

33) touchz : Zero length인 file을 생성





#### 출처
----------------------------
https://devanix.tistory.com/307 [┗System∑Sec†ion┛] <br>
 https://knight76.tistory.com/entry/spark-집합-함수-union-intersection-cartesian-subtract-join-cogroup-예제 [김용환 블로그(2004-2020)]<br>
https://excelsior-cjh.tistory.com/56 [EXCELSIOR]<br>
https://1004jonghee.tistory.com/entry/Apache-Spark란 [Hee'World]


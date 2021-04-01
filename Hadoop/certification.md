노트 패드 쓸수 있나 그럼 sqoop같은건 미리 적어놓고 그 후에도 처음꺼에서 조금씩 변형해가면서 복붙해서 시간아껴야겟다
	모든 걸 노트패드에 적고 옮겨서 실행해야됨
Sql문 컬럼명 띄워쓰기 안됨. Crime_type으로 해야함
Saveas는 경로 안에 classOf해서 compress하고 write은 sqlContext.setConf(“spark.sql.어쩌구”,””) 

# Sqoop
--connect --username --password --table

--as-textfile
--as-avrodatafile
--as-parquetfile


--compress
--compression-codec org.apache.hadoop.id.compress.SnappyCodec




--fields-terminated-by '\t'
--target-dir # 어떨땐 그냥 dir하잖아
-m 1 #이게 도대체 뭐냐

# sqlContext
val sqlContext = new org.apache.spark.sql.SQLContext(sc) 
import sqlContext.impIicits._ 
import org.apache.spark.sql._ 
# SQL
아주 똑똑하게 워드색기……..
.toDF()
registerTempTable(“”)
# avro
spark.read.format(“avro”).load(“경로”)
# parquet
sqlContext.setConf(“spark.sql.parquet.compression.codec”,”snappy”)
datafram.read.parquet(“경로”)
# text
sc.saveAsTextFile(“경로”)
import org.apache.hadoop.io.compress.SnappyCodec
sc.saveAsTextFile(“경로”,calssOf[snappyCodec])
# validating output
1. 
Hadoop fs -ls /user/crim/solution
Hadoop fs -get /user/crim/solution
Cd solution/
Ls -ltr
Gunzip part-00000.gz
Ls -ltr
View part-00000
2. 
val output = sc.textfile(“/user/crime/solution”)
output.collect().foreach(println)

# spark-spring-boot-starter
简单的创建spark连接对象，包括 SparkConf、SparkSession、JavaSparkContext、JavaStreamingContext 

使用：
1. 下载到本地，然后 mvn install
2. 需要的项目中在 pom.xml 中添加坐标，如
```
<!--spark-->
<dependency>
    <groupId>org.srp.spark</groupId>
    <artifactId>spark-spring-boot-starter</artifactId>
    <version>0.0.1-SNAPSHOT</version>
</dependency>
```
然后通过 Spring 的 @Autowired 引用对象，如
```
@Autowired
private SparkSession sparkSession;
```
3. 使用注意：
  * 尽量使用 @Autowired 来注入，而不是 @Resource
  * 涉及到的Spark版本为2.7.3(scala为2.11)，涉及到的hadoop版本为2.4.3。如需其他版本，修改pom.xml即可
  * 对spark提供的配置参数，也有一些规则，如下：
  ```
  1. 必须提供appname
  spark.appname=test

  2. 默认使用local模式，可以通过配置修改为使用集群
  spark.master=spark://xxx:7077

  3. 支持其他配置，不过需要将原有的 spark.xxx.xxx 配置模式，修改为 spark.props.xxx.xxx 才会被读取
    spark.props.serializer=org.apache.spark.serializer.KryoSerializer
    spark.props.executor.cores=4
    spark.props.executor.memory=4g
    spark.props.cores.max=60
    spark.props.local.dir=/tmp
    # 读写大量数据时需要稍微调优
    spark.props.network.timeout=10000000
    spark.props.executor.heartbeatInterval=10000000
    spark.props.memory.fraction=0.75
    spark.props.storage.memoryFraction=0.45
  4. 使用外部jar包时可以通过下面的方式引用，
    spark.jars[0]=/usr/software/spark-jar/jars/hbase-client-1.2.0.jar
    spark.jars[1]=/usr/software/spark-jar/jars/hbase-common-1.2.0.jar
    spark.jars[2]=/usr/software/spark-jar/jars/hbase-server-1.2.0.jar
    spark.jars[3]=/usr/software/spark-jar/jars/hbase-protocol-1.2.0.jar
  ```
  

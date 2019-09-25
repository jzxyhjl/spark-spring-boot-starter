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
  

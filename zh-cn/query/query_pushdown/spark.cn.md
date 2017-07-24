## 使用 Spark 查询引擎

Spark 是用于大数据处理的快速通用引擎，具有用于流计算，SPARK-SQL，机器学习和图形处理的内置模块。
## Query Pushdown 连接 spark
* Spark-sql-thrift 使用 HIVE JDBC 接口，支持jdbc接口的应用可以通过Hive-jdbc访问Spark进行数据查询。

* Download HIVE JDBC Driver
  1. 根据自己hadoop集群hive的版本下载对应版本的[hive-jdbc-version.jar](hive-jdbc.jarhttps://mvnrepository.com/artifact/org.apache.hive/hive-jdbc)，请确保使用的jdbc版本不要高于集群的hive版本。
  2. 下载[httpclient-version.jar](https://mvnrepository.com/artifact/org.apache.httpcomponents/httpclient)和[httpcore-version.jar](https://mvnrepository.com/artifact/org.apache.httpcomponents/httpcore)。

* 安装 JDBC
  1. 把下载好的jar包放到 `KAP_HOME/ext` 下面，以便让KAP在启动时可以加载 JDBC Driver 。

* 修改 `$KAP_HOME/conf/kylin.properties` ，添加以下配置。

  1. 配置 hive jdbc driver 和 Pushdown Runner:

     1. ```kylin.query.pushdown.runner-class-name=org.apache.kylin.query.adhoc.PushDownRunnerJdbcImpl```

     2. ```kylin.query.pushdown.jdbc.driver=org.apache.hive.jdbc.HiveDriver```


  2. 配置 JDBC URL

     1. 访问没有 kerberos 安全认证的 spark-sql-thrift 集群，例如(访问default库):

        ```kylin.query.pushdown.jdbc.url=jdbc:hive2://spark_host:spark_hs2_port/default```

     2. 访问带有 kerberos 安全认证的 spark-sql-thrift
        + 访问带有 kerberos 认证 spark-sql-thrift 需要 JDBC Client 端包含 spark-sql-thrift(principal=<Spark-Kerberos-Principal>)principal 在 jdbc url中，例如(访问 default 库):

           ```kylin.query.pushdown.jdbc.url=jdbc:hive2://spark_host:spark_hs2_port/default;principal=Spark-Kerberos-Principal```


        + 请确保kap能都读取到的hive-site.xml中打开了hive-server2的kerberos认证:
            ```
                   <property>
                       <name>hive.server2.authentication</name>
                       <value>kerberos</value>
                   </property>
             ```
         + 在初始化 hive-jdbc connection 前，kap 需要具有有效的 kerberos ticket，**请确保 klist 中存在有效的 principal** 能够访问spark-sql-thrift。
  3. 验证 thriftserver
     1. 启动 beeline ```${SPARK_HOME} or ${HIVE_HOME}/bin/beeline```。
     2. 使用 beeline 连接 Thrifterver ```!connect  kylin.query.pushdown.jdbc.url```。
     3. 使用简单sql测试可用。
  4. 验证测试
     1. 启动 kap，进行表查询。
     2. spark web 页面中能够找到刚才的查询，表示kap能够正常连接spark-sql-thrift。

      ![](query_pushdown_images/query_pushdown_spark.png)






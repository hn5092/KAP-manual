## 集成Kerberos
Kerberos 是一种支持票证身份验证的安全协议。如果KAP部署的平台开启了kerberos服务，需要通过本文的配置让KAP集成平台的kerberos服务运行。
### KAP 配置
KAP 的`$KYLIN_HOME/conf/kylin.properties`配置文件中，kerberos相关参数。

必选参数：
   
   - kap.kerberos.enabled : 是否启用kerberos认证，默认为false，可选true，false
   - kap.kerberos.platform : 认证平台，可选FI，Standard
   - kap.kerberos.principal : principal名称
   - kap.kerberos.keytab : keytab文件名
   
可选参数：
   
   - kap.kerberos.ticket.refresh.interval.minutes : ticket刷新周期，单位分钟，默认值720分钟
   - kap.kerberos.krb5.conf : kerberos配置文件名, 默认krb5.conf
   - kap.kerberos.cache : ticket cache文件名称, 默认kap_kerberos.cache
   
### 标准配置(非华为FusionInsight)
1. 需要在安装yarn的NodeManager的节点上，添加kerberos对应的用户。
   
   例如：
   kerberos用户kylin, 需要在NodeManager所在的节点的操作系统也拥有kylin用户。
2. 设置kerberos相关参数。

   - kap.kerberos.enabled=true
   - kap.kerberos.platform=Standard
   - kap.kerberos.principal={your principal name}
   - kap.kerberos.keytab={your keytab name}
   
3. 将认证keytab文件放到`$KYLIN_HOME/conf`目录下。   
   
### FI(华为FusionInsight)配置

1. 设置kerberos相关参数。

   - kap.kerberos.enabled=true
   - kap.kerberos.platform=FI
   - kap.kerberos.principal={your principal name}
   - kap.kerberos.keytab={your keytab name}

2. 配置FI机机账户，需要配置该用户拥有HDFS、HBase、Yarn、Spark、Hive、Kafka、Zookeeper相关权限，并将该账户(包含keytab和krb5.conf文件)导出。
FI 账户配置请参考：[FI配置机机账户](http://support.huawei.com/hedex/hdx.do?lib=EDOC1000130541YZG0106X&docid=EDOC1000130541&lang=zh&v=05&tocLib=EDOC1000130541YZG0106X&tocV=05&id=it_61_50_000061&tocURL=resources%252fadmin%255fguide%252fit%255f61%255f50%255f000061%252ehtml&p=t&fe=1&ui=3&keyword=%252525E7%25252594%252525A8%252525E6%25252588%252525B7&keyword=%252525E5%25252588%2525259B%252525E5%252525BB%252525BA&text=%2525253Cfont%25252Bcolor%2525253D%25252522%25252523B60005%25252522%2525253E%252525E5%25252588%2525259B%252525E5%252525BB%252525BA%2525253C%2525252Ffont%2525253E%2525253Cfont%25252Bcolor%2525253D%25252522%25252523B60005%25252522%2525253E%252525E7%25252594%252525A8%252525E6%25252588%252525B7%2525253C%2525252Ffont%2525253E)
[导出账户](http://support.huawei.com/hedex/hdx.do?lib=EDOC1000130541YZG0106X&docid=EDOC1000130541&lang=zh&v=05&tocLib=EDOC1000130541YZG0106X&tocV=05&id=it_61_50_000030&tocURL=resources%252fadmin%255fguide%252fit%255f61%255f50%255f000030%252ehtml&p=t&fe=1&ui=3&keyword=%252525E5%252525AF%252525BC%252525E5%25252587%252525BA&text=%2525253Cfont%25252Bcolor%2525253D%25252522%25252523B60005%25252522%2525253E%252525E5%252525AF%252525BC%252525E5%25252587%252525BA%2525253C%2525252Ffont%2525253EKeytab%252525E6%25252596%25252587%252525E4%252525BB%252525B6)

 机机账户需设置:
    - KAP期望读取的hive数据库  读权限
    - kylin.env.hdfs-working-dir 写权限
    - kylin.source.hive.database-for-flat-table 写权限
    
 KAP参数说明，请参考：
[KAP参数列表](http://docs.kyligence.io/v2.5/zh-cn/config/basic_settings.cn.html)

3. 将步骤2中导出的keytab文件以及配置文件krb5.conf放到`$KYLIN_HOME/conf`目录下。


### FI认证配置：
FI的认证配置有以下两种：
#### Cache认证

1. 新建jaas.conf文件，并放置`$KYLIN_HOME/conf` 目录下。

```
Client{
	com.sun.security.auth.module.Krb5LoginModule required
	useKeyTab=false
	useTicketCache=true
	storeKey=true
	debug=false;
};
```

#### Keytab认证
1. 配置kylin.properties,在beeline的连接字符串添加user.principal(对应kap.kerberos.principal参数)以及user.keytab(对应kap.kerberos.keytab参数)
2. 配置kylin.properties,添加kylin.engine.spark-conf.spark.yarn.principal(对kap.kerberos.principal参数)以及kylin.engine.spark-conf.spark.yarn.keytab(对应kap.kerberos.keytab参数)
3. 新建jaas.conf文件，并放置`$KYLIN_HOME/conf` 目录下。

```
Client{
	com.sun.security.auth.module.Krb5LoginModule required
	useKeyTab=true
	useTicketCache=false
	storeKey=true
	debug=false;
};
```
 



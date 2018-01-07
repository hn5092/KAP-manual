## 配置用户查询结果的导出权限

KAP系统管理人员可以通过配置`conf/kylin.properties`下的`kap.web.export.allow.admin`和`kap.web.export.allow.other`两个配置项来设置KAP查询用户的导出权限。

1. 设置`kap.web.export.allow.admin`为`false`后，将关闭ADMIN用户对查询结果的导出权限。ADMIN用户在Insight页面将不显示导出按钮，并且没有调用导出查询结果restful api的权限；
2. 设置`kap.web.export.allow.other`为`false`后，将关闭非ADMIN用户对查询结果的导出权限。非ADMIN用户在Insight页面将不显示导出按钮，并且没有调用导出查询结果restful api的权限。

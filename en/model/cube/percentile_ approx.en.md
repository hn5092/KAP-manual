## Approximate Percentile

Since KAP V2.5.4, there is a new function, percentile_approx, introduced, which was called percentile previously in KAP. Both of them have the same algorithm and result. This new function aims at (sub-)second latency for **approximate** percentile analytics SQL queries. In KAP, it has three return types: 'percentile(100)', 'percentile(1000)' and 'percentile(10000)'.

### percentile_approx

percentile_approx returns the value of below which a given percentage of observations in a group of observations fall. For example, the 20th percentile is the value below which 20% of the observations may be found. Its syntax is as below:

> percentile_approx({measure},p,B): measure is the measure to query; p is number between 0 to 1 with both included. B is to control the Approximate Accuracy. The higher the value is, the higher the accuracy of result will be. percentile_approx uses the interpolation method to determine the value of the pth percentile. 

The query example in KAP is as below:

```
SELECT seller_id, percentile_approx(price, 0.5)
FROM KYLIN_SALES
GROUP BY seller_id
```

### How to use

Firstly, in the third step of Cube creation, click **Add Measure** in the left corner to add a new measure.

![Add Measure](images/percentile_approximate/1.en.png)

Secondly, input your measure name, select **PENCENTILE_APPROX** as Expression, select Param Value, and then select return type 'percentile(100)', 'percentile(1000)' and 'percentile(10000)' on demand. By default, it will return 'percentile(10000)'. The return type means B listed in the above syntax. Higher value means higher accuracy.

![Select return type](images/percentile_approximate/return_type.en.png)

Thirdly, design and build Cube, then go to **Insight** page to simulate query. You will get the result as below.

![SQL query](images/percentile_approximate/cube_query.en.png)


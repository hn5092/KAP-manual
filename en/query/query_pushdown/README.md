# Query Pushdown

KAP supports query pushdown from version 2.4. When queries which cannot be fulfilled with customized Cubes bother you, you can simply leverage query pushdown to redirect the query to Spark SQL or Hive, making a trade-off  between query latency and query flexibility to obtain a better experience.

Continue reading:

[Trun on Query Pushdown](pushdown.en.md)

[Spark engine integration](spark.en.md)

[Impala engine integration](impala.en.md)


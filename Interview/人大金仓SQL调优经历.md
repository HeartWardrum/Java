使用`explain analyze`关键词

~~~sql
EXPLAIN ANALYZE 
SELECT round(SUM(COALESCE(xbmj, 0))::NUMERIC, 2)
FROM lyjcfx.resource_sl_2023
WHERE id IN ('d1f47f93-94f3-4098-aba0-ecc5e20ff2ad', 'cad11b9b-6225-4daa-a60f-9bef72ea8d2f');
~~~

发现是seq scan (全表查询)，没有用到索引，然后发现线上的表导入到本地后，主键索引丢失了。

将查询时间从单个sql 5s以上，调整到 20多ms


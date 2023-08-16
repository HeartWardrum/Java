# Oracle中特有

在select语句后面添加for update；可以实现图形化界面的增删改操作。

Oracle中的关联查询可以实现(+)的另一边全部展示

例如：

```sql
select * from teacher t ,department d where t.dno = d.dno(+);-- teacher表会全部展示
```

~~~sql
select sysdate from dual; -- sysdate 和 dual都是Oracle特有
~~~



### 自增长

Oracle中使用 序列 sequence

MySQL中使用auto_increment

## 分页

Oracle使用rownum

MySQL使用limit 起始条数，每页条数

## 系统时间

Oracle使用sysdate

select sysdate from dual;

MySQL使用now()

select now();

## 日期转字符串

Oracle使用to_char()将日期转字符串

MySQL使用date_format()将日期转字符串


## Oracle和MySQL的区别

### 宏观上

1. Oracle是大型数据库而MySQL是中小型；
2. Oracle收费，MySQL开源免费
3. Oracle支持大并发，大访问量，是[OLTP](#OLTP)的最好的工具
4. MySQL安装完成后占用的内存远远小于Oracle

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

## 补充

## OLTP

On-Line Transaction Processing联机事务处理过程，也成为面向交易的处理过程，其基本特征是前台接受的用户数据可以立即传送到计算中心进行处理，并且在很短的时间内给出处理结果，是对用户操作快速响应的方式之一。




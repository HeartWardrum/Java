## @ConfigurationProperties

https://www.cnblogs.com/tian874540961/p/12146467.html

用来注入配置

可以配合@Data来用

例如：

application.properties:

~~~yml
spring.datasource.url=jdbc:mysql://127.0.0.1:8888/test?useUnicode=false&autoReconnect=true&characterEncoding=utf-8
spring.datasource.username=root
spring.datasource.password=root
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
spring.datasource.type=com.alibaba.druid.pool.DruidDataSource
~~~


看这篇：

https://mp.weixin.qq.com/s?__biz=MzUyNTgzNDc3MQ==&mid=2247492544&idx=1&sn=cd10e75e54c1385df5197feba0dc7051&chksm=fa1aacbccd6d25aace4c97918400f1b17ce51d576625efccfa5087d739efed69a339e219a7aa&scene=21#wechat_redirect

本地项目见：

D:\java\MyProject\mybatisplus20231120







## 注解

## mapper接口

### @Mapper

加在mapper接口上

```java
@Mapper
public interface UserMapper extends BaseMapper<User> {
    //mapper接口必须要继承BaseMapper接口
    //实体类作为泛型
}
```

​	是mybatis注解，用来说明这是一个mapper，在mybatis中@Mapper需要和@Repository一起用，否则会出现无法自动注入的问题，而在mybatisplus中，这个问题得到了修复，单独使用@Mapper即可

## 实体类

### @Data

加在实体类上

~~~java
@Data
public class User { }
~~~



  @Data 注解的主要作用是提高代码的简洁，使用这个注解可以省去代码中大量的get()、 set()、 toString()等方法；

要使用 @Data 注解要先引入lombok：

~~~xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.4</version>
    <scope>provided</scope>
</dependency>
~~~



### @TableName("表名")

加在实体类上

```java
@Data
@TableName("user1120")  //表名对应数据库里的表名
public class User { }
```

如果不加这个注解，那么实体类的类名必须和数据库表名一毛一样，否则报错。

### @TableField("字段名")

加在属性上

```java
@Data
@TableName("user1120")  //表名对应数据库里的表名
public class User {

 @TableField("id")   //字段名对应数据库里的字段名
 private String uid;
}
```

如果不加这个注解，那么实体类的属性名必须和数据库字段名一毛一样，否则报错。

## resource类

### @RestController

包含了@ResponseBody和@Controller

@ResponseBody 方法返回值默认会被转换成JSON格式，并通过HTTP响应返回给客户端

@Controller 带有此注解的类将被视为控制器（Controller）

```java
@RestController
@RequestMapping("/user")
public class UserResource {
}
```

## service接口和serviceImpl实现类

### @Slf4j

**slf4j是一个日志标准，使用它可以完美的桥接到具体的日志框架，必要时可以简便的更换底层的日志框架，而不需要关心具体的日志框架的实现**

```java
@Service
@Slf4j
@Transactional
public class UserServiceImpl implements UserService {
}
```

### @Transactional

它能保证方法内多个数据库操作要么同时成功、要么同时失败




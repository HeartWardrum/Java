## JDBC ---- 这是java连接数据库的接口

通常需要使用 ` Class.forName(驱动类)` 来加载数据库驱动

接着获取`Connection`对象表示数据库的连接

然后获取`Statement`对象表示sql语句

最后获取`ResultSet`对象表示查询的结果集，它通过`Statement`对象调用`excuteQuery(Sql语句)`来执行获取

注意：以上对象在使用完毕后需要调用close方法来进行关闭

固定语句：

~~~java
public class HelloJdbc {

    public static void main(String[] args) {

        Connection conn = null;
        Statement stat = null;

        try {
            Class.forName("com.mysql.cj.jdbc.Driver");//加载驱动
            conn = DriverManager.getConnection("jdbc:mysql://192.168.77.100:3306/mysql", "root", "123456");
            stat = conn.createStatement();//获取sql语句的操作对象
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

}
~~~



例子：

~~~java
public static void main(String[] args) {

        Connection conn = null;
        Statement stat = null;
        ResultSet rest = null;

        try {
            Class.forName("com.mysql.cj.jdbc.Driver");//这是第一步 加载驱动 Driver类的全类名
            conn = DriverManager.getConnection("jdbc:mysql://192.168.77.100:3306/mysql", "root", "123456");//这是第二步 getConnection("jdbc:mysql://xxx.xxx.xxx.xxx:3306/数据库名,"账号","密码")
            stat = conn.createStatement();//这是第三步 获取sql语句的操作对象
            String sql = "select s.sno,s.sname,date_format(s.birthday,'%Y-%m-%d %H:%i:%s') birthday \n" +
                    "from stu0720 s";
            rest = stat.executeQuery(sql);//执行sql语句，返回一个结果集
            while(rest.next()){//遍历每一行
                int sno = rest.getInt("sno");
                String sname = rest.getString("sname");
                String birthday = rest.getString("birthday");
                System.out.println(sno + "," + sname + "," + birthday);
            }
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        }finally {
            try {
                if(rest != null)
                {
                    rest.close();
                }
                if(stat != null){
                    stat.close();
                }
                if(conn != null){
                    conn.close();
                }
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
~~~

# 2022年7月21日

ResultSetMetaData

JDBC 获取结果集中列相关的信息

我们可以通过ResultSet对象调用`getMetaData()`获取该对象

它提供了一些常用方法：

`getColumnCount() ---- 获取列数`

`getColumnName(列数) ---- 获取列名`

对于`ResultSet`来讲，我们还可以通过`getObject(列数)`来获取列值

## 查询

~~~java
public static void main(String[] args) {

        Connection conn = null;
        Statement stat = null;
        ResultSet rest = null;
        ResultSetMetaData rsmd = null;//获取结果集中的列相关的信息

        try {
            Class.forName("com.mysql.cj.jdbc.Driver");//这是第一步 加载驱动 Driver类的全类名
            conn = DriverManager.getConnection("jdbc:mysql://192.168.77.100:3306/mysql", "root", "123456");//这是第二步 getConnection("jdbc:mysql://xxx.xxx.xxx.xxx:3306/数据库名,"账号","密码")
            stat = conn.createStatement();//这是第三步 获取sql语句的操作对象
            String sql = "select s.sno,s.sname,date_format(s.birthday,'%Y-%m-%d %H:%i:%s') birthday,s.age \n" +
                    "from stu0720 s";
            rest = stat.executeQuery(sql);//执行sql语句，返回一个结果集
            rsmd = rest.getMetaData();//获取列相关的信息
            int columnCount = rsmd.getColumnCount();
            while (rest.next()) {
                for (int i = 1; i <= columnCount; i++) {
                    String columnName = rsmd.getColumnName(i);
                    Object columnValue = rest.getObject(i);
                    System.out.print(columnName + "=" + columnValue + "    ");

                }
                System.out.println();

            }
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            try {
                if (rest != null) {
                    rest.close();
                }
                if (stat != null) {
                    stat.close();
                }
                if (conn != null) {
                    conn.close();
                }
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
~~~

## 增删改

我们可以调用`Statement`对象的`executeUpdate(sql语句)`来执行增删改操作

使用JDBC操作Mysql数据库，如果需要操作中文数值，则url后面需要添加参数：`?characterEncoding=utf-8`

~~~java
public static void myJdbc() {

        Connection conn = null;
        Statement stat = null;
        ResultSet rest = null;
        ResultSetMetaData rsmd = null;//获取结果集中的列相关的信息

        try {
            Class.forName("com.mysql.cj.jdbc.Driver");//这是第一步 加载驱动 Driver类的全类名
            conn = DriverManager.getConnection("jdbc:mysql://192.168.77.100:3306/mysql?characterEncoding=utf-8", "root", "123456");//这是第二步 getConnection("jdbc:mysql://xxx.xxx.xxx.xxx:3306/数据库名,"账号","密码")
            stat = conn.createStatement();//这是第三步 获取sql语句的操作对象
            String sql = "insert into stu0720(sno,sname,birthday,age) \n"
                    + "values(null,'李寻欢','2001-03-23',21)"; //增删改的语句写在这里面
            int i = stat.executeUpdate(sql);
            System.out.println("成功操作了：" + i + "条记录");
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            try {
                if (rest != null) {
                    rest.close();
                }
                if (stat != null) {
                    stat.close();
                }
                if (conn != null) {
                    conn.close();
                }

            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
~~~

## 登录

~~~java
public static void main(String[] args) {
        System.out.println(isLogin("admin","123456"));
    }

    public static boolean isLogin(String username, String password) {

        Connection conn = null;
        Statement stat = null;
        ResultSet rest = null;
        int cou = 0;
        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
            conn = DriverManager.getConnection("jdbc:mysql://192.168.77.100:3306/mysql?characterEncoding=utf-8", "root", "123456");
            stat = conn.createStatement();
            String sql = "select count(*) cou from my_user u\n" +
                    "where u.username = '" + username + "'\n" +
                    "and u.password = '" + password + "'";
            rest = stat.executeQuery(sql);
            while(rest.next()){
                cou = rest.getInt("cou");
            }

        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        }finally{
            try {
                if(conn != null)
                    conn.close();
                if(stat != null)
                    stat.close();
                if(rest != null)
                    rest.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        return cou > 0;
    }
~~~

## 防止sql注入

`PreparedStatement` ----这是一个Statement 接口的子接口，它可以执行sql语句的时候，防止用户进行sql注入

具体步骤：

1. 在sql中需要传入参数的地方使用`?`
2. 将sql语句传入Connection对象的`prepareStatement()`方法得到当前的`PreparedStatement`对象
3. 使用`PreparedStatement`对象调用`setXxx()`方法依次对每一个`?`进行参数绑定，`?`从1开始
4. 调用`executeQuery()`完成sql执行并返回ResultSet结果集

~~~java
public static void main(String[] args) {
        //System.out.println(isLogin("admin","123' or '1' = '1"));
        System.out.println(isLogin("admin", "123456"));
    }

    public static boolean isLogin(String username, String password) {

        Connection conn = null;
        PreparedStatement pstat = null;
        ResultSet rest = null;
        int cou = 0;

        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
            conn = DriverManager.getConnection("jdbc:mysql://192.168.77.100:3306/mysql?characterEncoding=utf8", "root", "123456");
            //pstat = conn.createStatement();
            String sql = "select count(*) cou from my_user u where u.username = ? \n" +
                    "and u.password = ? ";
            pstat = conn.prepareStatement(sql);
            pstat.setString(1, username);
            pstat.setString(2, password);
            rest = pstat.executeQuery();//不需要再传入sql
            while (rest.next()) {
                cou = rest.getInt("cou");
            }
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            try {
                if (conn != null)
                    conn.close();
                if (pstat != null)
                    pstat.close();
                if (rest != null)
                    rest.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        return cou > 0;
    }
~~~

## MD5加密

我们可以调用`DigestUtils.md5Hex(明文字符串)`  来得到对应的密文字符串

~~~java
public static void main(String[] args) {
        String s1 = "123456";
        s1 = DigestUtils.md5Hex(s1);
        System.out.println(s1);
    }
~~~

## Sha256加密

还可以调用`DigestUtils.shaHex(明文字符串)`来得到对应的密文字符串

~~~java
        String s2 = "123456";
        s2 = DigestUtils.sha256Hex(s2);
        System.out.println(s2);  
~~~

## 工具类(最终版)

~~~java
package com.iweb.test;

import java.sql.*;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class JdbcUtil {

    static Connection conn = null;
    static PreparedStatement pstat = null;
    static ResultSet rest = null;


    //获取数据库连接
    private static Connection getConnection() {
        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
            conn = DriverManager.getConnection("jdbc:mysql://192.168.77.100:3306/mysql?characterEncoding=utf8", "root", "123456");
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return conn;
    }


    //关闭资源
    private static void closeResource() {
        try {
            if (rest != null)
                rest.close();
            if (pstat != null)
                pstat.close();
            if (conn != null)
                conn.close();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }


    //查询的jdbc
    public static <E> List<Map<String, Object>> queryBySql(String sql, E... e) {
        getConnection();
        List<Map<String, Object>> list = new ArrayList<>();

        try {
            pstat = conn.prepareStatement(sql);
            for (int i = 0; i < e.length; i++) {
                pstat.setObject(i + 1, e[i]);
            }
            rest = pstat.executeQuery();
            ResultSetMetaData rsmd = rest.getMetaData();
            while (rest.next()) {
                Map<String, Object> map = new HashMap<>();
                for (int i = 0; i < rsmd.getColumnCount(); i++) {
                    map.put(rsmd.getColumnName(i + 1), rest.getObject(i + 1));
                }
                list.add(map);
            }
        } catch (SQLException ex) {
            ex.printStackTrace();
        } finally {
            closeResource();
            return list;
        }
    }


    //增删改的JDBC
    public static <E> int updateBySql(String sql, E... e) {
        getConnection();//获取连接
        int res = 0;

        try {
            pstat = conn.prepareStatement(sql);
            for (int j = 0; j < e.length; j++) {
                pstat.setObject(j + 1, e[j]);
            }
            res = pstat.executeUpdate();

        } catch (SQLException ex) {
            ex.printStackTrace();
        } finally {
            closeResource();
        }
        return res;
    }
}
~~~

~~~java
//测试查询
public static void main(String[] args) {
        String sql = "select * from fiction";
        List<Map<String, Object>> list = new ArrayList<>();
        list = JdbcUtil.quaryBySql(sql);
        System.out.println(list);
    }
~~~

~~~java
//测试增删改
    public static void main(String[] args) {
        String sql = "insert into my_user values(?,?,'123456')";
        int i = JdbcUtil.updateBySql(sql, "1008", "wangwu");
        System.out.println("成功操作：" + i + "条数据");
    }
~~~

### Oracle数据库的JDBC配置

1. jar:  ojdbc6_g.jar
2. 驱动类： oracle.jdbc.driver.OracleDriver
3. URL: jdbc.oracle:thin:@ip地址:1521:数据库名

~~~java
Class.forName("oracle.jdbc.driver.OracleDriver");
            conn = DriverManager.getConnection("jdbc:oracle:thin:@192.168.77.100:1521:helowin","scott","123456");
~~~


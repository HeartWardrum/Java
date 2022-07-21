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

我们可以调用Statement对象的executeUpdate(sql语句)来执行增删改操作

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
                    + "values(null,'李寻欢','2001-03-23',21)";
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




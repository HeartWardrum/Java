## JDBC ---- 这是java连接数据库的接口

通常需要使用  Class.forName(驱动类) 来加载数据库驱动

接着获取Connection对象表示数据库的连接

然后获取Statement对象表示sql语句

最后获取ResultSet对象表示查询的结果集，它通过Statement对象调用excuteQuery(Sql语句)来执行获取

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
            while(rest.next()){
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


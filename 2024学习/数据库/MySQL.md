Windows的MySQL启动方式



打开管理员cmd

启动服务

~~~shell
net start mysql
~~~

登录MySQL

~~~shell
mysql -uroot -p
~~~

切换数据库

~~~shell
use mysql;
~~~

关闭MySQL

~~~shell
exit
~~~

关闭服务

~~~shell
net stop mysql
~~~


**`J2EE     JAVAEE     Java web`**

# JavaEE
http://127.0.0.1:8080  测试TomCat首页

## servlet
Servlet ---- 是个接口
servlet ---- 是一个实现了Servlet接口的Java类，他可以接收浏览器的请求，返回给浏览器响应

servlet生命周期的相关方法：
1. 构造方法：用来创建当前servlet对象
2. init方法：用来初始化当前servlet对象
3. service方法：用来处理一个前端的请求
4. destroy方法：销毁当前servlet对象

servlet核心配置文件
所有的请求和java类都是靠 `web.xml`对应的
每一个`<servlet>`表示一个servlet，它包含`<servlet-name>` 和 `<servlet-class>`

- `<servlet-name> `是我们自己起的servlet名字
- `<servlet-class>` 是我们自己写的servlet类的全类名


每个`<servlet>` 都有`<servlet-mapping>` 与之对应
` <servlet-mapping>` 中包含`<servlet-name> `和 `<url-pattern>`
- `<servlet-mapping>`中的`<servlet-name> `与 `<servlet>`中的`<servlet-name>` 对应  值相等就完事了
- `<url-pattern>`指的是请求名 通常以`/`开头

当我们启动tomcat之后，我们的javaEE项目就发布了，它等待着前端发起以下格式的请求：
http://ip地址:端口/web应用名/请求名

~~~java
package com.iweb.homework;

import javax.servlet.*;
import java.io.IOException;

/**
 * @Author HearWardrum
 * 联系方式：tianxiayifan@qq.com
 * @Date 2022-08-01/0001
 * 描述：测试Servlet生命周期
 */

public class Test2 implements Servlet {
    public Test2() {
        System.out.println("构造Test2");
    }

    @Override
    public void init(ServletConfig servletConfig) throws ServletException {
        System.out.println("初始化Test2");
    }

    @Override
    public ServletConfig getServletConfig() {
        return null;
    }

    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
        System.out.println("Test2收到一个请求");
    }

    @Override
    public String getServletInfo() {
        return null;
    }

    @Override
    public void destroy() {

    }
}
~~~
~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>com.iweb.homework.Test2</servlet-class>
    </servlet>

    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/my1threquest</url-pattern>
    </servlet-mapping>

</web-app>

//  运行后在弹出页面的地址栏后面补上my1threquest 回车 即可构造初始化Servlet并接收到请求
~~~



### `<load-on-startup>`
在`<servlet>`中，表示当前servlet对象被创建和初始化的时机，如果取值为0 或正整数，则随着tomcat启动，自动完成创建和初始化
注意：数值越小(>=0)的`<load-on-startup>` 它的`<servlet>`越先被创建和初始化
~~~xml
    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>com.iweb.homework.Test2</servlet-class>
        <load-on-startup>0</load-on-startup>
    </servlet>

~~~

注意：一个`<servlet>`可以对应多个`<servlet-mapping>`，只需要`<servlet-name> `一致即可，它们的`<url-pattern>`不一样，所以接收到不同的请求，可以进入同一个方法

~~~xml
    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>com.iweb.homework.Test2</servlet-class>
        <load-on-startup>0</load-on-startup>
    </servlet>

    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/my1threquest</url-pattern>
    </servlet-mapping>

    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/my2ndrequest</url-pattern>
    </servlet-mapping>
    
    // 运行后在弹出页面的地址栏后面补上my1threquest或者my2ndrequest 回车 都会使test2收到一个请求
~~~

注意：在`<servlet-mapping>`中，可以使用通配符表示任意请求，通配符的格式：
1. /*
2. /
3. *.后缀名(后缀名随便写)
~~~xml
    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>com.iweb.homework.Test2</servlet-class>
        <load-on-startup>0</load-on-startup>
    </servlet>

    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/*</url-pattern>
    </servlet-mapping>
    
    // 运行后在弹出页面的地址栏后面随便补上点什么 回车 都会使test2收到一个请求
~~~

~~~xml
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>*.do</url-pattern>
    </servlet-mapping>
    // 运行后在弹出页面的地址栏后面 补上 随便什么.do 回车 都会使test2收到一个请求

~~~

### servletConfig
这是当前servlet的大管家，它可以获取servlet方方面面的信息
例如：
1. `<init-param>`表示servlet的初始化参数
	我们可以通过  该对象.getInitParameter(参数名)  获取参数值
2. getServletName() ---- 获取当前servlet名字
	~~~java
    @Override
    public void init(ServletConfig servletConfig) throws ServletException {
        System.out.println("初始化Test2");
        String str = servletConfig.getInitParameter("username");
        System.out.println(str);
        String servletName = servletConfig.getServletName();
        System.out.println(servletName);

    }
	~~~
	~~~xml
	    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>com.iweb.homework.Test2</servlet-class>
        <init-param>
            <param-name>username</param-name>
            <param-value>root</param-value>
        </init-param>
        <load-on-startup>0</load-on-startup>
    </servlet>
    // 在初始化Servlet时 输出 :
    // root
    // hello 
	~~~
3. getServletContext() ---- 获取当前web应用的对象
	注意：ServletContext对象表示当前web应用的对象，它可以获取当前web应用方方面面的信息
	~~~java
	    @Override
    public void init(ServletConfig servletConfig) throws ServletException {
        ServletContext sc = servletConfig.getServletContext();
        String user = sc.getInitParameter("username");
        System.out.println(user);
    }
	~~~
	~~~xml
	    <context-param>
        <param-name>username</param-name>
        <param-value>Admin</param-value>
    </context-param>
    // 在初始化Servlet时 输出 :
    //Admin
	~~~
	
### ServletContext对象的相关信息：
`<context-param>` ---- 当前web应用的初始化参数
我们可以通过ServletContext对象调用
getInitParameter(参数名) 来获取它的参数值
getRealPath(文件的类路径) ---- 获取到该文件部署后的绝对路径
	~~~java
	    @Override
    public void init(ServletConfig servletConfig) throws ServletException {
        System.out.println("初始化Test2");
        ServletContext sc = servletConfig.getServletContext();
        String path = sc.getRealPath("/hi.html");
        System.out.println(path);
    }
	~~~
getContextPath() ---- 获取的是当前web应用的根目录

浏览器页面向后端java类发请求的方式：
1. 地址栏直接写url
2. `<a>`标签超链接
		~~~xml
	    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>com.iweb.homework.Test2</servlet-class>
        <init-param>
            <param-name>username</param-name>
            <param-value>root</param-value>
        </init-param>
        <load-on-startup>0</load-on-startup>
    </servlet>

    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>*.do</url-pattern>
    </servlet-mapping>
	~~~
	~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<h1>我是一个标题</h1>
<a href="abc.do?age=18">发一个请求</a>
</body>
</html>

	~~~
	~~~java
	    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
        System.out.println("Test2收到一个请求");
        String age = servletRequest.getParameter("age");
        System.out.println(age);
    }
    //点一下超链接发一个请求
    //输出参数值18
	~~~

3. `<form>`表单提交

请求的url可以携带参数，格式：
1. url?参数名1=参数值1&参数名2=参数值2
2. 在`<form>`中的表单控件上，name属性对应参数名，value属性对应参数值

后端Java类中，我们可以使用  ServletRequest对象.getParameter(参数名)  来获取参数值

面试题：
提交方式get和post的区别
get请求 ---- 请求参数是跟在url地址后面的
	所有的<a>都是get请求
post请求 ---- 请求参数是封装在消息体中的
	<form>的method可以指定其post，如果不指定，则默认为get
注意：get请求的参数的长度不能超过1k，post请求没有长度限制

ServletResponse
返回响应
我们可以通过该对象调用getWrite()得到PrintWrite对象，然后再调用PrintWrite对象的print()方法往浏览器打印需要返回的内容

HttpServletRequest
它是ServletRequest的子接口，我们在实际发送请求的过程中，前端传递给后端的全部都是HttpServletRequest对象，所以我们可以将ServletRequest向下转型为HttpServletRequest对象，然后可以调用它新增加的方法：
getMethod() ---- 获取当前请求的请求方式，返回GET或POST
getServletContext() ---- 直接获取当前web应用的ServletContext
getServletPath() ---- 获取当前请求的请求名


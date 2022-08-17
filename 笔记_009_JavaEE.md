---
title:  笔记_009_JavaEE
tag: 
	- javaEE
categories: 
	- java
---
**`J2EE     JAVAEE     Java web`**

# JavaEE
http://127.0.0.1:8088  测试TomCat首页

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
每一个`<servlet>`标签表示一 个servlet，它包含`<servlet-name>` 和 `<servlet-class>`

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

#### 1. `<init-param>`

表示servlet的初始化参数

我们可以通过  该对象.getInitParameter(参数名)  获取参数值

#### 2. getServletName() 

---- 获取当前servlet名字

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

#### 3. getServletContext() 

---- 获取当前web应用的对象

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

### 浏览器页面向后端java类发请求的方式：

1. 地址栏直接写url
2. `<a>`标签超链接
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<h1 style="color:gold;">我是一个标题</h1>
<a href="abc.do?age=18">发一个请求</a>
</body>
</html>


```java

    @Override
public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
    System.out.println("Test2收到一个请求");
    String age = servletRequest.getParameter("age");
    System.out.println(age);
}
//点一下超链接发一个请求
//输出参数值18
```

3. `<form>`表单提交

请求的url可以携带参数，格式：
1. url?参数名1=参数值1&参数名2=参数值2
2. 在`<form>`中的表单控件上，name属性对应参数名，value属性对应参数值

### ServletRequest
后端Java类中，我们可以使用  ServletRequest对象.getParameter(参数名)  来获取参数值

### 面试题：提交方式get和post的区别
get请求 ---- 请求参数是跟在url地址后面的
	所有的`<a>`都是get请求
post请求 ---- 请求参数是封装在消息体中的

`<form>`的method属性可以指定其为post，如果不指定，则默认为get

注意：get请求的参数的长度不能超过1k，post请求没有长度限制

### ServletResponse
返回响应
我们可以通过该对象调用getWrite()得到PrintWrite对象，然后再调用PrintWrite对象的print()方法往浏览器打印需要返回的内容

~~~java
    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
        System.out.println("Test2收到一个请求");
        PrintWriter pw = servletResponse.getWriter();
        pw.print("hello");
    }
~~~

HttpServletRequest
它是ServletRequest的子接口，我们在实际发送请求的过程中，前端传递给后端的全部都是HttpServletRequest对象，所以我们可以将ServletRequest向下转型为HttpServletRequest对象，然后可以调用它新增加的方法：
getMethod() ---- 获取当前请求的请求方式，返回GET或POST
getServletContext() ---- 直接获取当前web应用的ServletContext
getServletPath() ---- 获取当前请求的请求名
getContextPath() ---- 获取的是当前web应用的根目录

# 日期：2022-08-02

## HttpServlet

这是一个抽象类，它实现了Servlet接口，并且将ServletRequest和ServletResponse转型成了HttpServletRequest和HttpServletResponse

然后调用HttpServletRequest的getMethod方法判断当前请求是GET还是POST，从而为我们提供了doGet()和doPost()方法

对于我们编程来讲，我们只需要继承HttpServlet类并重写doXxx方法即可，我们可以专注于我们的业务逻辑

~~~java
public class Test1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("来了一个get请求");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("来了一个post请求");
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
        <servlet-name>test1</servlet-name>
        <servlet-class>com.iweb.test.Test1</servlet-class>
    </servlet>

    <servlet-mapping>
        <servlet-name>test1</servlet-name>
        <url-pattern>/test1</url-pattern>
    </servlet-mapping>

</web-app>
~~~

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<a href="test1">我是test1</a>
<br/>
<form action="test1" method="post">
    <button>提交</button>
</form>
</body>
</html>
~~~

## JSP

JavaServer Pages

将前后端混合编写的一种技术，混合编写的代码写在.jsp的文件中，页面上静态展示的内容使用html编写，动态展示的数据使用java编写。java代码在jsp页面上需要用<%%>包起来
~~~jsp
<%--
  Created by IntelliJ IDEA.
  User: lenovo
  Date: 2022-08-02/0002
  Time: 10:25
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<h3>这是我的以一个jsp页面</h3>
<%
    System.out.println("hello jsp!");
%>
</body>
</html>
~~~
### out.print();
---- 将指定内容打印在浏览器页面上
~~~jsp
<%@ page import="java.util.Date" %><%--
  Created by IntelliJ IDEA.
  User: lenovo
  Date: 2022-08-02/0002
  Time: 10:25
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<h3>这是我的以一个jsp页面</h3>
<%
    Date date = new Date();
    out.print(date);
%>
</body>
</html>
~~~

### jsp的本质

本质是servlet 是后端技术

### jsp九大隐含对象

隐含对象指的是在jsp中没有定义而可以直接使用的对象

1. request ---- HttpServletRequest的对象,它表示当前JSP页面打开的这次请求
2. response ---- HttpServletResponse的对象
3. pageContext ---- PageContext的对象，它表示当前页面，它可以获取其他8个隐含对象
4. session ---- HttpSession的对象，它表示一次会话（浏览器的打开到关闭）
5. application ---- ServletContext的对象，它表示当前的web应用
6. config ---- ServletConfig对象，它表示当前jsp翻译出来的那个servlet中的ServletConfig对象
7. out ---- JspWriter的对象，可以直接把字符串打印在浏览器上
8. page ---- 表示当前JSP翻译出来的那个servlet类的对象
9. exception ---- 表示jsp中发生的各种异常

### JSP表达式

<%=表达式内容%> ---- 可以直接将java变量或表达式打印在页面上

~~~jsp
<%@ page import="java.util.Date" %><%--
  Created by IntelliJ IDEA.
  User: lenovo
  Date: 2022-08-02/0002
  Time: 10:25
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<h3>这是我的以一个jsp页面</h3>
<%
    Date date = new Date();
    out.print(date);
%>
<br/>
<br/>
<%=date%>
<br/>
<br/>
<%
    String age = request.getParameter("age");
    out.print(age);
%>

<%
    int intage = Integer.valueOf(age);
    if (intage > 18) {
        out.print("您已成年");
    } else {
        out.print("未成年人给爷死！");
    }

%>
</body>
</html>

~~~

需要打印的内容以静态页面的方式呈现：（效果同上面一样）
~~~jsp
<%@ page import="java.util.Date" %><%--
  Created by IntelliJ IDEA.
  User: lenovo
  Date: 2022-08-02/0002
  Time: 10:25
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<h3>这是我的以一个jsp页面</h3>
<%
    Date date = new Date();
    out.print(date);
%>
<br/>
<br/>
<%=date%>
<br/>
<br/>
<%
    String age = request.getParameter("age");
    out.print(age);
%>

<%
    int intage = Integer.valueOf(age);
    if (intage >= 18) {
%>

您已成年
<%
} else {
%>
未成年人给爷死！
<%
    }

%>
</body>
</html>
~~~

### JSP的注释
以`<%--`开头   以`--%>`结尾

### 域对象
pageContext, request, session, application 四个隐含对象成为域对象，它们可以调用setAttribute(键，值)   进行存值
getAttribute(键)   进行取值
removeAttribute(键)    进行删除
~~~jsp
<%--
  Created by IntelliJ IDEA.
  User: HeartWardrum
  Date: 2022-08-02/0002
  Time: 11:22
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<h1>test2.jsp</h1>
<%
    pageContext.setAttribute("pageKey", "pageValue");
    request.setAttribute("requestKey", "requestValue");
    session.setAttribute("sessionKey", "sessionValue");
    application.setAttribute("applicationKey", "applicationValue");
%>

<%
    application.removeAttribute("applicationKey");
%>



<%=pageContext.getAttribute("pageKey")%>
<br/>
<%=request.getAttribute("requestKey")%>
<br/>
<%=session.getAttribute("sessionKey")%>
<br/>
<%=application.getAttribute("applicationKey")%>

</body>
</html>
~~~

### 域对象的作用范围：
pageContext ---- 当前页面
request ---- 一次请求
session ---- 一次会话
application ---- 整个web应用

test2：
~~~jsp
<%--
  Created by IntelliJ IDEA.
  User: HeartWardrum
  Date: 2022-08-02/0002
  Time: 11:22
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<h1>test2.jsp</h1>
<%
    pageContext.setAttribute("pageKey", "pageValue");
    request.setAttribute("requestKey", "requestValue");
    session.setAttribute("sessionKey", "sessionValue");
    application.setAttribute("applicationKey", "applicationValue");
%>

<%=pageContext.getAttribute("pageKey")%>
<br/>
<%=request.getAttribute("requestKey")%>
<br/>
<%=session.getAttribute("sessionKey")%>
<br/>
<%=application.getAttribute("applicationKey")%>

<br/>
<a href="test3.jsp">跳转到test3页面</a>

</body>
</html>
~~~

test3：
~~~jsp
<%--
  Created by IntelliJ IDEA.
  User: HeartWardrum
  Date: 2022-08-02/0002
  Time: 11:40
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<%=pageContext.getAttribute("pageKey")%>
<br/>
<%=request.getAttribute("requestKey")%>
<br/>
<%=session.getAttribute("sessionKey")%>
<br/>
<%=application.getAttribute("applicationKey")%>

</body>
</html>
~~~
### 请求转发和重定向
这是两种用来实现java类跳转到下一个目标的资源的技术
#### 第一种：请求转发的步骤
1. 定义一个String 存放目标资源的路径
2. 通过当前request对象调用getRequestDispatcher(路径) 获取RequestDispatcher对象
3. 使用RequestDispatcher对象调用forward(request,response)完成转发
~~~jsp
<%--
  Created by IntelliJ IDEA.
  User: HeartWardrum
  Date: 2022-08-02/0002
  Time: 13:34
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<h1>测试请求转发和重定向</h1>
<br/>
<a href="testForward">请求转发</a>

</body>
</html>
~~~
~~~jsp
<%--
  Created by IntelliJ IDEA.
  User: HeartWardrum
  Date: 2022-08-02/0002
  Time: 13:35
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<h1>成功页面</h1>
</body>
</html>
~~~
~~~java
public class TestForward extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("即将开始请求转发");
        String path = "/success.jsp";
        RequestDispatcher rd = req.getRequestDispatcher(path);
        rd.forward(req, resp);//完成转发
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
        <servlet-name>testForward</servlet-name>
        <servlet-class>com.iweb.test.TestForward</servlet-class>
    </servlet>

    <servlet-mapping>
        <servlet-name>testForward</servlet-name>
        <url-pattern>/testForward</url-pattern>
    </servlet-mapping>

</web-app>
~~~
#### 第二种：重定向
1. 定义一个String 存放目标资源的路径 (路径要从web根目录开始)
2. 利用当前response对象调用sendRedirect(路径) 完成重定向
~~~jsp
<%--
  Created by IntelliJ IDEA.
  User: HeartWardrum
  Date: 2022-08-02/0002
  Time: 13:34
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<h1>测试请求转发和重定向</h1>
<br/>
<a href="testForward">请求转发</a>
<br/>
<a href="testRedirect">重定向</a>
</body>
</html>
~~~
~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <servlet>
        <servlet-name>testRedirect</servlet-name>
        <servlet-class>com.iweb.test.TestRedirect</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>testRedirect</servlet-name>
        <url-pattern>/testRedirect</url-pattern>
    </servlet-mapping>

</web-app>
~~~
~~~java
public class TestRedirect extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("即将开始重定向");
        String path = "/test20220802/success.jsp";
        resp.sendRedirect(path);


    }
}
~~~

##### 请求转发和重定向的区别：
- 请求转发在转发前和转发后，是同一次请求
- 重定向在重定向前和重定向后是两次不同的请求

###### 细节上的区别：
1. 目标路径的斜杠含义不同
	转发的时候，/ 表示web应用的根目录
	重定向的时候，/ 表示web站点的根目录
	

注意：http请求的格式：
http://ip:端口  ---- web站点的根目录
web站点的根目录 + web应用的名字 ---- web应用的根目录
web应用的根目录 + 请求名 ---- 完整的http请求

2. url地址栏显示的内容不同：
	转发的时候显示的是初次发起的请求名
	重定向的时候显示的是最终目标资源的文件名
	
3. 转发前和转发后是同一个request对象
	重定向前和重定向后是两个不同的request对象
~~~java
public class TestForward extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("即将开始请求转发");
        req.setAttribute("myKey01","myValue01");
        String path = "/success.jsp";
        RequestDispatcher rd = req.getRequestDispatcher(path);
        rd.forward(req, resp);//完成转发
    }
}
~~~
~~~java
public class TestRedirect extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("即将开始重定向");
        req.setAttribute("myKey02", "myValue02");
        String path = "/test20220802/success.jsp";
        resp.sendRedirect(path);
    }
}
~~~
~~~jsp
<%--
  Created by IntelliJ IDEA.
  User: HeartWardrum
  Date: 2022-08-02/0002
  Time: 13:34
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<h1>测试请求转发和重定向</h1>
<br/>
<a href="testForward">请求转发</a>
<br/>
<a href="testRedirect">重定向</a>
</body>
</html>
~~~

4. 转发只能转到当前web应用以内的资源
	重定向可以重定向到任何资源
~~~java
public class TestForward extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("即将开始请求转发");
        req.setAttribute("myKey01","myValue01");
        String path = "http://www.bing.com";
        RequestDispatcher rd = req.getRequestDispatcher(path);
        rd.forward(req, resp);//完成转发
    }
}
~~~
~~~java
public class TestRedirect extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("即将开始重定向");
        req.setAttribute("myKey02", "myValue02");
        String path = "http://www.bing.com";
        resp.sendRedirect(path);
    }
}
~~~

注意：请求转发和重定向 不仅仅可以跳转到下一个页面，它还可以跳转进入下一个servlet
~~~java
public class TestForward extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("即将开始请求转发");
        req.setAttribute("myKey01","myValue01");
        String path = "/test";
        RequestDispatcher rd = req.getRequestDispatcher(path);
        rd.forward(req, resp);//完成转发
    }
}
~~~
~~~java
public class TestRedirect extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("即将开始重定向");
        req.setAttribute("myKey02", "myValue02");
        String path = "/test20220802/test";
        resp.sendRedirect(path);
    }
}
~~~
~~~xml
    <servlet>
        <servlet-name>test</servlet-name>
        <servlet-class>com.iweb.test.Test</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>test</servlet-name>
        <url-pattern>/test</url-pattern>
    </servlet-mapping>
~~~
~~~java
public class Test extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("我是下一个java类");
    }
}
~~~

### 发请求的路径问题
我们通过<a>的href属性和<form>的action属性发请求，最好写成以下路径格式：
`<%=request.getContextPath()%>/请求名`
否则有可能会带来路径的错误
~~~java
<%--
  Created by IntelliJ IDEA.
  User: HeartWardrum
  Date: 2022-08-02/0002
  Time: 13:34
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<h1>测试请求转发和重定向</h1>
<br/>
<a href="<%=request.getContextPath()%>/testForward">请求转发</a>
<br/>
<a href="<%=request.getContextPath()%>/testRedirect">重定向</a>
<form action="<%=request.getContextPath()%>/testRedirect">

</form>
</body>
</html>
~~~
### 表单提交中文乱码问题
在request.getParameter(""); 之前添加：
request.setCharacterEncoding("utf-8"); 即可
~~~java
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        req.setCharacterEncoding("utf-8");
        String username = req.getParameter("username");
        System.out.println(username);
    }
~~~

### MVC开发模型
M ---- Model
V ---- View
C ---- Control

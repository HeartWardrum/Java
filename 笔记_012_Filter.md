---
title:  笔记_012_Filter过滤器
tag: 
	- java
categories: 
	- java
---

# Filter

通常来讲，过滤器指的是一个实现类Filter接口（Tomcat中的）的java类，它可以通过web.xml来配置所拦截的资源
过滤器有生命周期相关的方法：
init() ---- 初始化
doFilter() ---- 拦截到一个请求
destory() ---- 销毁

**注意**：在web.xml 中需要配置过滤器拦截怎样的请求
`<filter>`下包含`<filter-name>`和`<filter-class>`
`<filter-class>`指向过滤器类的全类名
`<filter-mapping>`下包含`<filter>`对应的`<filter-name>`和需要拦截的`<url-pattern>`
~~~java
package com.iweb.test;


import javax.servlet.*;
import java.io.IOException;
import java.util.logging.LogRecord;

/**
 * @Author HearWardrum
 * 联系方式：tianxiayifan@qq.com
 * @Date 2022-08-12/0012
 * 描述：
 */

public class HelloFilter implements Filter {

    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        System.out.println("当前过滤器初始化了");
    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        System.out.println("拦截到了一个去test1的请求！");
    }

    @Override
    public void destroy() {
        System.out.println("当前过滤器销毁了");
    }
}
~~~
~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <filter>
        <filter-name>hello</filter-name>
        <filter-class>com.iweb.test.HelloFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>hello</filter-name>
        <url-pattern>/test1.jsp</url-pattern>
    </filter-mapping>

</web-app>
~~~
~~~jsp
<%--
  Created by IntelliJ IDEA.
  User: HeartWardrum
  Date: 2022-08-12/0012
  Time: 8:45
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
    <title>$Title$</title>
  </head>
  <body>
  <a href="<%=request.getContextPath()%>/test1.jsp">test1</a>
  </body>
</html>
~~~
~~~jsp
<%--
  Created by IntelliJ IDEA.
  User: HeartWardrum
  Date: 2022-08-12/0012
  Time: 8:46
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<h1>test1页面</h1>
</body>
</html>
~~~
## 放行
如果在doFilter()方法拦截到请求之后需要放行，则可以调用它的参数FilterChain对象的doFilter(request,response)对象进行放行
~~~java
    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        System.out.println("拦截到了一个去test1的请求！");
        filterChain.doFilter(servletRequest, servletResponse);//放行

    }
~~~

**注意**：过滤器可以拦截一个去往servlet的请求

过滤器的初始化参数：在`<filter>`中，可以配置`<init-param>`，其中包含`<param-name>`和`<param-value>`我们在init方法中可以使用filterConfig对象调用getInitParameter(参数名)得到参数值

**注意**：servlet 能干的事情，filter都能干，过滤器可以取代servlet，除此之外，它还善于过滤
~~~java
package com.iweb.test;

import javax.servlet.*;
import java.io.IOException;

/**
 * @Author HearWardrum
 * 联系方式：tianxiayifan@qq.com
 * @Date 2022-08-12/0012
 * 描述：
 */

public class MyFilter implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        String username = filterConfig.getInitParameter("username");
        System.out.println(username);

        ServletContext sc = filterConfig.getServletContext();
        String user = sc.getInitParameter("user");
        System.out.println(user);
    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        System.out.println("拦截MyServlet");
        filterChain.doFilter(servletRequest, servletResponse);
    }

    @Override
    public void destroy() {

    }
}
~~~
~~~java
package com.iweb.test;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * @Author HearWardrum
 * 联系方式：tianxiayifan@qq.com
 * @Date 2022-08-12/0012
 * 描述：
 */

public class MyServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("来了一个请求");
    }


}
~~~
~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <context-param>
        <param-name>user</param-name>
        <param-value>root</param-value>
    </context-param>

    <filter>
        <filter-name>hello</filter-name>
        <filter-class>com.iweb.test.HelloFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>hello</filter-name>
        <url-pattern>/test1.jsp</url-pattern>
    </filter-mapping>


    <filter>
        <filter-name>myfilter</filter-name>
        <filter-class>com.iweb.test.MyFilter</filter-class>
        <init-param>
            <param-name>username</param-name>
            <param-value>admin</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>myfilter</filter-name>
        <url-pattern>/myServlet</url-pattern>
    </filter-mapping>


    <servlet>
        <servlet-name>myServlet</servlet-name>
        <servlet-class>com.iweb.test.MyServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>myServlet</servlet-name>
        <url-pattern>/myServlet</url-pattern>
    </servlet-mapping>


</web-app>
~~~
~~~jsp
<%--
  Created by IntelliJ IDEA.
  User: HeartWardrum
  Date: 2022-08-12/0012
  Time: 8:45
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>$Title$</title>
</head>
<body>
<a href="<%=request.getContextPath()%>/test1.jsp">test1</a>
<br/>
<a href="<%=request.getContextPath()%>/myServlet">发个请求</a>
</body>
</html>
~~~

过滤器支持多层过滤，多个过滤器可以拦截同一个请求，每个过滤器放行会放行到下一层过滤器，如果当前是最后一层，则放行到目标资源
注意：多层过滤的时候，先后顺序是由web.xml中的`<filter-mapping>`配置的先后顺序决定的

# 练习

创建两个web应用的初始化参数，分别记录用户名和密码，画一个登录页面，再画一个成功页面，输入账号密码，点击登录直接跳转到成功页面

创建两个过滤器，第一个专门过滤账号对不对，对就放行，不对就转发回登录页面，提升账号错误

如果放行，那就来到第二个过滤器，校验密码，对就放行，不对就转发回登录页面，提升密码错误

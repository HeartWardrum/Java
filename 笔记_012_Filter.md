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




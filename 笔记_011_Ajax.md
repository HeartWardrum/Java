# Ajax

Asynchronous JavaScript And Xml

无需刷新页面，而使前后端通信的技术，在用户不知情的情况下，前端向后端发送请求，得到后端的响应，局部地更新页面的一种技术

Ajax总是在JS的事件中发请求

原生态的Ajax代码是在围绕真XMLHttpRequest对象展开的，我们可以调用它的open方法装载数据，调用它的send方法发送请求，调用它的onreadystatechange()方法接收来自后端的响应

原生态的Ajax写法
~~~jsp
<%--
  Created by IntelliJ IDEA.
  User: HeartWardrum
  Date: 2022-08-10/0010
  Time: 8:55
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>$Title$</title>
    <script type="text/javascript">
        window.onload = function () {
            var helloText = document.getElementById("hello");
            helloText.onkeyup = function () {
                var req = new XMLHttpRequest();
                var url = "<%=request.getContextPath()%>/helloajax";
                var method = "GET";
                req.open(method, url);
                req.send(null);//get请求不用传参
                req.onreadystatechange = function () {
                    if (req.readyState == 4) {
                        //已经接收到了后端来的反馈
                        if (req.status == 200 || req.status == 304) {
                            document.getElementById("message").innerHTML = req.responseText;
                        }
                    }
                }
            }
        }
    </script>
</head>
<body>
<input type="text" id="hello"/><span id="message" style="color:red;"></span>
</body>
</html>
~~~

~~~jsp
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">


    <servlet>
        <servlet-name>helloajax</servlet-name>
        <servlet-class>com.iweb.test.HelloAjax</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>helloajax</servlet-name>
        <url-pattern>/helloajax</url-pattern>
    </servlet-mapping>


</web-app>
~~~
~~~java
package com.iweb.test;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;



public class HelloAjax extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("Hello Ajax");
        PrintWriter pw = resp.getWriter();
        pw.print("Hello Ajax");
    }


}
~~~

# JSON
---- 这是一种数据格式，经常用于前后端交互的时候，来封装传递的数据，格式：
以`{`开头，以`}`结尾，中间是键值对，键和值以冒号分割，键值对之间以逗号分割
在js中，`Json对象.键 ` 可以得到值
~~~jsp
<%--
  Created by IntelliJ IDEA.
  User: HeartWardrum
  Date: 2022-08-10/0010
  Time: 9:32
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
    <script type="text/javascript">
        window.onload = function () {
            var obj = {
                "name": "Tom", "age": 18,
                "address": {"city": "nanjin", "school": "南信大"},
                "teach": function () {
                    alert("java");
                }
            };
            alert(obj.name);
            alert(obj.age);
            alert(obj.address.school);
            obj.teach();
            
        }
    </script>
</head>
<body>

</body>
</html>

~~~
**注意**：Json中，值可以是任何类型，也可以是一个json，还可以是一个函数

# eval函数

---- 这是一个js的函数，它可以将字符串中的js代码解析出来

~~~jsp
<%--
  Created by IntelliJ IDEA.
  User: HeartWardrum
  Date: 2022-08-10/0010
  Time: 9:32
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
    <script type="text/javascript">
        window.onload = function () {
         
            var testEval = "alert(\"Hello\")";
            eval(testEval);
            
            var testJsonStr = "{\"name\":\"iweb\"}";
            var jsonObj = eval("(" + testJsonStr + ")");
            alert(jsonObj.name);
        }
    </script>
</head>
<body>

</body>
</html>
~~~

**注意**：如果使用eval函数解析JSON字符串，则需要在左右两边分别拼上 `"("`  和 `")"`

~~~jsp
            var testJsonStr = "{\"name\":\"iweb\"}";
            var jsonObj = eval("(" + testJsonStr + ")");
            alert(jsonObj.name);
~~~

## JSON字符串转字符对象

使用`JSON.parse(json字符串) ` 即可

~~~jsp
<%--
  Created by IntelliJ IDEA.
  User: HeartWardrum
  Date: 2022-08-10/0010
  Time: 9:32
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
    <script type="text/javascript">
        window.onload = function () {
            var obj = {
                "name": "Tom", "age": 18,
                "address": {"city": "nanjin", "school": "南信大"},
                "teach": function () {
                    alert("java");
                }
            };
          
            var testJsonStr = "{\"name\":\"iweb\"}";
            // var jsonObj = eval("(" + testJsonStr + ")");
            // alert(jsonObj.name);
            var jsonObj = JSON.parse(testJsonStr);
            alert(jsonObj.name);


        }
    </script>
</head>
<body>

</body>
</html>

~~~

# `JQuery`框架将原生态的Ajax代码封装成一个叫作`$.ajax()`

然后它再次对$.ajax()进行二次封装，提供给我们以下三个函数：
1. load() ---- 由某元素节点调用，返回值自动填充在该元素节点的子元素位置,它如果传一个url，则发起get请求，如果传一个url和一个json格式的参数对象，则发起post请求
~~~jsp
<%--
  Created by IntelliJ IDEA.
  User: HeartWardrum
  Date: 2022-08-10/0010
  Time: 10:35
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
    <script type="text/javascript" src="<%=request.getContextPath()%>/jquery-3.2.1.js"></script>
    <script type="text/javascript">
        $(function () {
            $("#hello").keyup(function () {
                var str = $(this).val();
                var param = {
                    "name": str
                };
                $("#message").load("<%=request.getContextPath()%>/helloajax", param);
            })
        })
        <%--$(function () {--%>
        <%--    $("#hello").keyup(function () {--%>
        <%--        var str = $(this).val();--%>
        <%--            $("#message").load("<%=request.getContextPath()%>/helloajax?name=" + str);--%>
        <%--    })--%>
        <%--})--%>
    </script>
</head>
<body>
<input type="text" id="hello"/><span id="message" style="color:red;"></span>

</body>
</html>
~~~
~~~java
package com.iweb.test;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

/**
 * @Author HearWardrum
 * 联系方式：tianxiayifan@qq.com
 * @Date 2022-08-10/0010
 * 描述：
 */

public class HelloAjax extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        req.setCharacterEncoding("utf-8");
        System.out.println("Hello Ajax");
        String name = req.getParameter("name");
        resp.setCharacterEncoding("utf-8");
        resp.setContentType("text/html");
        PrintWriter pw = resp.getWriter();
        pw.print("Hello " + name);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("我是一个post请求");
        req.setCharacterEncoding("utf-8");
        String name = req.getParameter("name");
        resp.setCharacterEncoding("utf-8");
        resp.setContentType("text/html");
        PrintWriter pw = resp.getWriter();
        pw.print("hello " + name);
    }
}
~~~

2. $.get(url,json参数,function回调方法) ---- 它只能发起get请求，后端的响应封装在回调方法的参数中
~~~jsp
<%--
  Created by IntelliJ IDEA.
  User: HeartWardrum
  Date: 2022-08-10/0010
  Time: 10:35
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
    <script type="text/javascript" src="<%=request.getContextPath()%>/jquery-3.2.1.js"></script>
    <script type="text/javascript">
        $(function () {
            $("#hello").keyup(function () {
                var str = $(this).val();
                var param = {
                    "name": str
                };
                var url = "<%=request.getContextPath()%>/helloajax";
                <!--$("#message").load("
                <%=request.getContextPath()%>/helloajax", param);-->
                $.get(url, param, function (data) {
                    $("#message").html(data);
                })
            })
        })
        <%--$(function () {--%>
        <%--    $("#hello").keyup(function () {--%>
        <%--        var str = $(this).val();--%>
        <%--            $("#message").load("<%=request.getContextPath()%>/helloajax?name=" + str);--%>
        <%--    })--%>
        <%--})--%>
    </script>
</head>
<body>
<input type="text" id="hello"/><span id="message" style="color:red;"></span>

</body>
</html>
~~~

3. $.post(url,json参数,function回调方法) ---- 它只能发起post请求，后端的响应封装在回调方法的参数中
**注意**：如果ajax返回的内容带有中文，那么请在返回之前添加：
~~~java
        resp.setCharacterEncoding("utf-8");
        resp.setContentType("text/html");
~~~

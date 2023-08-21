---
title:  笔记_011_Ajax
tag: 
	- java
categories: 
	- java
---

# Ajax

Asynchronous JavaScript And Xml

无需刷新页面，而使前后端通信的技术，在用户不知情的情况下，前端向后端发送请求，得到后端的响应，局部地更新页面的一种技术

Ajax总是在JS的事件中发请求

原生态的Ajax代码是围绕XMLHttpRequest对象展开的，我们可以
1. 调用它的open方法装载数据
2. 调用它的send方法发送请求
3. 调用它的onreadystatechange()方法接收来自后端的响应

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
        resp.setContentType("text/html");//设置发送到客户端的响应的内容类型
        PrintWriter pw = resp.getWriter();
        pw.print("Hello " + name);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("我是一个post请求");
        req.setCharacterEncoding("utf-8");//请求转码  ----- 中文请求不乱码
        String name = req.getParameter("name");//获取
        resp.setCharacterEncoding("utf-8");//响应转码  ----- 打印中文不乱码
        resp.setContentType("text/html");//设置发送到客户端的响应的内容类型
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

## fastjson
这是由阿里巴巴公司提供的，将java对象转json字符串的框架，我们只需要使用
JSONObject.toJSONString(json对象);   ---- 就可以得到该对象对应的JSON字符串

使用方法：
-  导入fastjson-1.2.53.jar包
~~~java
    public static void main(String[] args) {
        Student s = new Student("1001", "张三", "20", "男");
        String json = JSONObject.toJSONString(s);
        System.out.println(json);
        //输出
        //{"gender":"男","sage":"20","sname":"张三","sno":"1001"}

    }
~~~
**注意**：如果有一个集合对象，那么fastjson将提供一个JSON数组字符串来表示
~~~java
    public static void main(String[] args) {
        Student s = new Student("1001", "张三", "20", "男");
        String json = JSONObject.toJSONString(s);
        //System.out.println(json);

        Student s2 = new Student("1002", "张三", "20", "男");
        Student s3 = new Student("1003", "李四", "20", "男");
        Student s4 = new Student("1004", "王五", "20", "男");
        List<Student> list = new ArrayList<>();
        list.add(s);
        list.add(s2);
        list.add(s3);
        list.add(s4);
        String json2 = JSONObject.toJSONString(list);
        System.out.println(json2);


    }
~~~

~~~java
    public static void main(String[] args) {
        Student s = new Student("1001", "张三", "20", "男");
        String json = JSONObject.toJSONString(s);
        //System.out.println(json);

        Student s2 = new Student("1002", "张三", "20", "男");
        Student s3 = new Student("1003", "李四", "20", "男");
        Student s4 = new Student("1004", "王五", "20", "男");
        List<Student> list = new ArrayList<>();
        list.add(s);
        list.add(s2);
        list.add(s3);
        list.add(s4);
        String json2 = JSONObject.toJSONString(list);
        //System.out.println(json2);

        Teacher teacher = new Teacher("5000", "王小明", "30", list);
        String json3 = JSONObject.toJSONString(teacher);
        System.out.println(json3);


    }
~~~

在项目中，我们首先迅速打开页面，展示静态内容，然后我们可以使用Ajax发起二次请求，查询数据库，将数据库填充在静态页面上，缓解因为性能问题造成用户长时间等待空白页面的焦虑
~~~java
package com.iweb.test;

/**
 * @Author HearWardrum
 * 联系方式：tianxiayifan@qq.com
 * @Date 2022-08-11/0011
 * 描述：
 */

public class Student {
    private String sno;
    private String sname;
    private String sage;
    private String gender;


    public Student() {
    }

    public Student(String sno, String sname, String sage, String gender) {
        this.sno = sno;
        this.sname = sname;
        this.sage = sage;
        this.gender = gender;
    }

    public String getSno() {
        return sno;
    }

    public void setSno(String sno) {
        this.sno = sno;
    }

    public String getSname() {
        return sname;
    }

    public void setSname(String sname) {
        this.sname = sname;
    }

    public String getSage() {
        return sage;
    }

    public void setSage(String sage) {
        this.sage = sage;
    }

    public String getGender() {
        return gender;
    }

    public void setGender(String gender) {
        this.gender = gender;
    }
}
~~~
~~~java
package com.iweb.test;

import com.alibaba.fastjson.JSONObject;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * @Author HearWardrum
 * 联系方式：tianxiayifan@qq.com
 * @Date 2022-08-11/0011
 * 描述：
 */

public class StudentServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doPost(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String path = req.getServletPath();
        switch (path) {
            case "/toEdit.student":
                req.getRequestDispatcher("/edit.jsp").forward(req, resp);
                break;
            case "/queryDate.student":
                query(req, resp);
                break;
            default:
                break;

        }
    }

    protected void query(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        String sno = req.getParameter("sno");
        System.out.println("根据学号：" + sno + "开始查询数据库");
        Student s = new Student("1001", "张三", "20", "男");
        String res = JSONObject.toJSONString(s);
        resp.setCharacterEncoding("utf-8");
        resp.getWriter().print(res);

    }

}
~~~
~~~xml
    <servlet>
        <servlet-name>student</servlet-name>
        <servlet-class>com.iweb.test.StudentServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>student</servlet-name>
        <url-pattern>*.student</url-pattern>
    </servlet-mapping>
~~~
~~~jsp
<%--
  Created by IntelliJ IDEA.
  User: HeartWardrum
  Date: 2022-08-11/0011
  Time: 11:55
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<script type="text/javascript" src="<%=request.getContextPath()%>/jquery-3.2.1.js"></script>
<script type="text/javascript">
    $(function () {
        var url = "<%=request.getContextPath()%>/queryDate.student";
        var param = {
            "sno": ${param.sno}
        };
        $.post(url, param, function (data) {
            var jsonObj = JSON.parse(data);
            $("#sno").val(jsonObj.sno);
            $("#sname").val(jsonObj.sname);
            $("#sage").val(jsonObj.sage);
            $("#gender").val(jsonObj.gender);
        })
    })


</script>
<h1>我是编辑页面</h1>
学号：<input id="sno" name="sno" value=""/>
<br/><br/>
姓名：<input id="sname" name="sname" value=""/>
<br/><br/>
年龄：<input id="sage" name="sage" value=""/>
<br/><br/>
性别： <input id="gender" name="gender" value=""/>
<br/><br/>
<input type="submit" value="提交">

</body>
</html>
~~~
~~~jsp
<%--
  Created by IntelliJ IDEA.
  User: HeartWardrum
  Date: 2022-08-11/0011
  Time: 9:46
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>$Title$</title>
</head>
<body>
<a href="<%=request.getContextPath()%>/toEdit.student?sno=1001">编辑</a>
</body>
</html>
~~~
以上代码实现分布式加载页面，先显示静态布局，再等两秒后加载数据


**`J2EE JAVAEE Java web`**
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

每个`<servlet>` 都有`<servlet-mapping>` 与之对应` <servlet-mapping>` 中包含`<servlet-name> `和 `<url-pattern>`
- `<servlet-name> `和 `<servlet>`中的`<servlet-name>` 对应  `<url-pattern>`指的是请求名

当我们启动tomcat之后，我们的javaEE项目就发布了，它等待着前端发起以下格式的请求：
http://ip地址:端口/web应用名/请求名

### `<load-on-startup>`
在`<servlet>`中，表示当前servlet对象被创建和初始化的时机，如果取值为0 或正整数，则随着tomcat启动，自动完成创建和初始化
注意：数值越小的`<load-on-startup>` 它的`<servlet>`越先被创建和初始化

注意：一个`<servlet>`可以对应多个`<servlet-mapping>`，只需要`<servlet-name> `一致即可，它们的`<url-pattern>`不一样，所以接收到不同的请求，可以进入同一个方法

注意：在`<servlet-mapping>`中，可以使用通配符表示任意请求，通配符的格式：
1. /*
2. /
3. *.后缀名

### servletConfig
这是当前servlet的大管家，它可以获取servlet方方面面的信息
例如：
1. `<init-param>`表示servlet的初始化参数
	我们可以通过  该对象.getInitParameter(参数名)  获取参数值
2. getServletName() ---- 获取当前servlet名字
3. getServletContext() ---- 获取当前web应用的对象
	注意：Servlet Context对象表示当前web应用的对象，它可以获取当前web应用方方面面的信息
	
### ServletContext对象的相关信息：
`<context-param>` ---- 当前web应用的初始化参数
我们可以通过ServletContext对象调用
getInitParameter(参数名) 来获取它的参数值
getRealPath(文件的类路径) ---- 获取到该文件部署后的绝对路径
getContextPath() ---- 获取的是当前web应用的根目录

浏览器页面向后端java类发请求的方式：
1. 地址栏直接写url
2. `<a>`标签超联集
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



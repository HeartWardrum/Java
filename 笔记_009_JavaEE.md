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
我们可以通过ServletContext对象调用getInitParameter(参数名) 来获取它的参数值
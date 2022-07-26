# JavaScript

JS的代码都是通过一系列的事件调用方法来执行的

方法通常写在`<script type="text/javascript">`中

定义方法格式：function 方法名(){....}



常用事件：

### onclick ---- 鼠标点击事件

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			function hello() {
				alert("hello js!"); /*弹窗函数*/
			}
		</script>
	</head>
	<body>
		<input type="button" value="hello" onclick="hello()" />
	</body>
</html>
~~~

弹出一个对话框：alert(内容字符串)

### onload ---- 窗体加载事件

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			function hello() {
				alert("hello js!"); /*弹窗函数*/
			}
		</script>
	</head>
	<body onload="hello()">		/*刷新页面自动触发事件*/
		<input type="button" value="hello"/>
	</body>
</html>

~~~

### onChange ---- 值发生修改事件

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			function textChange(i) {
				alert("值已修改,新的值是：" + i);
			}
		</script>
	</head>
	<body>
		<input type="text" onchange="textChange(this.value)" />
	</body>
</html>
~~~

注意：在js中，this表示当前元素节点。this.属性  表示当前元素节点的属性值

### onKeyDown ---- 键被按下

### onKeyUp ---- 键被按下后松开

### onmouseenter ---- 鼠标移动到当前控件上

### onmouseleave ---- 鼠标离开当前控件

### window.onload=function(){} ---- 窗体已加载

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			window.onload = function() {
				alert("窗体已加载");
			}
		</script>
	</head>
	<body>
	</body>
</html>
~~~

在窗体加载事件中，我们可以通过获取的   元素节点.事件=function(){....}  来完成指定操作

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			window.onload = function() {
				var btns = document.getElementsByTagName("button");
				// alert(btns.length);
				btns[0].onclick = function() {
					alert("我是第一个按钮");
				}
				btns[1].onclick = function() {
					alert("我是第er个按钮");
				}
			}
		</script>
	</head>
	<body>
		<button type="button">我是一个按钮</button>
		<button type="button">我也是一个按钮</button>
	</body>
</html>
~~~

### 在js中获取元素节点的方法

1. document.getElementsByTagName(元素节点名) ---- 获取当前页面上某元素节点的数组

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			window.onload = function() {
				var btns = document.getElementsByTagName("button");
				alert(btns.length);
			}
		</script>
	</head>
	<body>
		<button type="button">我是一个按钮</button>
		<button type="button">我也是一个按钮</button>
	</body>
</html>
~~~

注意：该方法可以由指定的某个元素节点来调用，那么得到的结果就是该元素节点下的指定子元素数组

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			window.onload = function() {
				var btns = document.getElementsByTagName("button");
				// alert(btns.length);
				btns[0].onclick = function() {
					alert("我是第一个按钮");
				};
				btns[1].onclick = function() {
					alert("我是第二个按钮");
				};

				var btn3 = document.getElementById("btn3");
				btn3.onclick = function() {
					alert("我是第三个按钮");
				};


				var lis = document.getElementsByTagName("li");
				alert(lis.length);

				var city = document.getElementById("city");
				var cityLis = city.getElementsByTagName("li");
				alert(cityLis.length);

			}
		</script>
	</head>
	<body>
		<button>我是一个按钮</button>
		<button>我也是一个按钮</button>
		<button id="btn3">我也是三个按钮</button>
		<ul id="city">
			<li>北京</li>
			<li>上海</li>
			<li>广州</li>
			<li>南京</li>
		</ul>
		<br>
		<ul id="game">
			<li>英雄联盟</li>
			<li>星际争霸</li>
			<li>魔兽世界</li>
		</ul>
	</body>
</html>

~~~



2. document.getElementById(id值) ---- 根据id获取当前元素节点

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			window.onload = function() {
				var btns = document.getElementsByTagName("button");
				// alert(btns.length);
				btns[0].onclick = function() {
					alert("我是第一个按钮");
				};
				btns[1].onclick = function() {
					alert("我是第二个按钮");
				};

				var btn3 = document.getElementById("btn3");
				btn3.onclick = function() {
					alert("我是第三个按钮");
				};
			}
		</script>
	</head>
	<body>
		<button>我是一个按钮</button>
		<button>我也是一个按钮</button>
		<button id="btn3">我也是三个按钮</button>
	</body>
</html>
~~~

3. document.getElementsByName(name值) ---- 根据name属性获取对应的元素数组

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			window.onload = function() {
				var types = document.getElementsByName("type");
				alert(types.length);

			}
		</script>
	</head>
	<body>
		<p>请选择类型</p>
		城市<input type="radio" name="type" />
		游戏<input type="radio" name="type" checked="checked" />
	</body>
</html>

~~~

4. document.getElementByClassName(class值) ---- 根据class属性获取对应的元素数组

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			window.onload = function() {
				var dels = document.getElementsByClassName("delete");
				alert(dels.length);
			}
		</script>
	</head>
	<body>
		<a href="#" class="delete">删除</a>
		<a href="#" class="delete">删除</a>
		<a href="#" class="delete">删除</a>
	</body>
</html>
~~~



我们可以通过  元素节点.属性名  获得属性值

我们可以通过  元素节点.属性名=新值  来改变属性值

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			window.onload = function() {				
				var textNode = document.getElementById("text1");
				alert(textNode.value);
				textNode.value = "abd";
			}
		</script>
	</head>
	<body>
		<input type="text"  id="text1" value="hello" />
	</body>
</html>
~~~

### childNodes ---- 获取某元素节点下的所有子节点，包括文本节点和元素节点

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			window.onload = function() {
				var btns = document.getElementsByTagName("button");
				// alert(btns.length);
				btns[0].onclick = function() {
					alert("我是第一个按钮");
				};
				btns[1].onclick = function() {
					alert("我是第二个按钮");
				};

				var btn3 = document.getElementById("btn3");
				btn3.onclick = function() {
					alert("我是第三个按钮");
				};


				var lis = document.getElementsByTagName("li");
				// alert(lis.length);

				var city = document.getElementById("city");
				var cityLis = city.getElementsByTagName("li");
				// alert(cityLis.length);

				var types = document.getElementsByName("type");
				//alert(types.length);

				var dels = document.getElementsByClassName("delete");
				// alert(dels.length);

				var textNode = document.getElementById("text1");
				//alert(textNode.value);
				textNode.value = "abd";

				var cityChilds = city.childNodes;
				alert(cityChilds.length);
			}
		</script>
	</head>
	<body>
		<ul id="city">
			<li>北京</li>
			<li>上海</li>
			<li>广州</li>
			<li>南京</li>
		</ul>
		<br>
		<ul id="game">
			<li>英雄联盟</li>
			<li>星际争霸</li>
			<li>魔兽世界</li>
		</ul>
	</body>
</html>

~~~


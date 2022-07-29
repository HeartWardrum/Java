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

### onchange ---- 值发生修改事件

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

注意：在js中，this表示当前元素节点。`this.属性 ` 表示当前元素节点的属性值

### onkeydown ---- 键被按下

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			function myFunction() {
				alert("键已按下");
			}
		</script>
	</head>
	<body>
		<input type="text" onkeydown="myFunction()">
	</body>
</html>
~~~

### onkeyup ---- 键被按下后松开

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			function myFunction() {
				alert("键已按下,然后松开了");
			}
		</script>
	</head>
	<body>
		<input type="text" onkeyup="myFunction()">
	</body>
</html>
~~~

### onmouseenter ---- 鼠标移动到当前控件上

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			function myFunction() {
				alert("鼠标移上来了");
			}
		</script>
	</head>
	<body>
		<input type="text" onmouseenter="myFunction()">
	</body>
</html>
~~~

### onmouseleave ---- 鼠标离开当前控件

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			function myFunction() {
				alert("鼠标离开了");
			}
		</script>
	</head>
	<body>
		<input type="text" onmouseleave="myFunction()">
	</body>
</html>
~~~

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

在窗体加载事件中，我们可以通过获取的   `元素节点.事件=function(){....} ` 来完成指定操作

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			window.onload = function() {

				var btns = document.getElementsByTagName("button");
				btns[0].onclick = function() {
					alert("我是第一个按钮");
				};
				btns[1].onclick = function() {
					alert("我是第二个按钮");
				};

			}
		</script>
	</head>
	<body>
		<button>我是一个按钮</button>
		<button>我也是一个按钮啊啊啊啊</button>
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
				var lis = document.getElementsByTagName("li");
				alert(lis.length);

				var city = document.getElementById("city");
				var cityLis = city.getElementsByTagName("li");
				alert(cityLis.length);
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



我们可以通过  `元素节点.属性名`  获得属性值

我们可以通过  `元素节点.属性名=新值`  来改变属性值

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
				var city = document.getElementById("city");
				var cityLis = city.getElementsByTagName("li");


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

如何获取文本？

`元素节点.firstChild.nodeValue;`

注意：`元素节点.firstChild.nodeValue=新值`  可以改变文本内容

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			window.onload = function() {
				var city = document.getElementById("city");
				var cityLis = city.getElementsByTagName("li");

				//var bjtext = cityLis[0].firstChild.nodeValue;
				var bjNode = cityLis[0];
				alert(bjNode);
				var bjTextNode = bjNode.firstChild;
				alert(bjTextNode);
				var bjText = bjTextNode.nodeValue;
				alert(bjText);
                  cityLis[0].firstChild.nodeValue = "hello 北京";
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

### 遍历

~~~html
				for (var i = 0; i < lis.length; i++) {
					var liNode = lis[i];
					alert(liNode.firstChild.nodeValue);
				}
~~~

~~~html
				for (var i = 0; i < lis.length; i++) {
					lis[i].onclick = function() {
						alert(this.firstChild.nodeValue);
					}
				}
~~~

### document.createElement(元素节点名) ---- 创建一个元素节点

`父节点.appendChild(新节点) `---- 将新创建的节点挂在某个父节点下

~~~html
				var myLi = document.createElement("li");
				city.appendChild(myLi);
~~~

### document.createTextNode(文本内容) --- 创建一个文本节点

我们需要使用   元素节点.appendChild(文本节点)  将新创建的文本节点挂在指定的元素节点下

~~~html
				var myText = document.createTextNode("南京");
				myLi.appendChild(myText);
~~~

对于单选框和复选框的选中状态，我们可以在js中使用check属性来获取，它是一个boolean值 true表示选中false表示未选中

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			window.onload = function() {
				
				var btn4 = document.getElementById("btn4");
				btn4.onclick=function(){
					var types = document.getElementsByName("type");
					for(var i=0;i<types.length;i++){
						alert(types[i].value+ ":" + types[i].checked);
					}
				}
				
			}
		</script>
	</head>
	<body>
		<p>请选择类型</p>
		城市<input type="radio" name="type" value="city"/>
		游戏<input type="radio" name="type" checked="checked" value="game"/>
		<br>
		<button id="btn4">检查选中状态</button>
	</body>
</html>

~~~

## 多选框

全选框  可复用

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			window.onload = function() {
				document.getElementById("checkedAll").onclick = function() {
					var hobbys = document.getElementsByName("hobby");
					for (var i = 0; i < hobbys.length; i++) {
						hobbys[i].checked = this.checked;
					}
				}


				var items = document.getElementsByName("hobby");
				for (var j = 0; j < items.length; j++) {
					items[j].onclick = function() {
						var num = 0;
						for (var k = 0; k < items.length; k++) {

							if (items[k].checked) {
								num++;
							}

						}
						document.getElementById("checkedAll").checked = (num == items.length);
					}
				}


			}
		</script>
	</head>
	<body>


		<p>请选择你的爱好：</p>
		全选<input type="checkbox" id="checkedAll" />
		足球<input type="checkbox" name="hobby" id="" value="football" />
		篮球<input type="checkbox" name="hobby" id="" value="basketball" />
		乒乓球<input type="checkbox" name="hobby" id="" value="pingpong" />
		羽毛球<input type="checkbox" name="hobby" id="" value="badminton" />

	</body>
</html>

~~~

# js第二天

### 删除元素节点

`父节点.removeChild(子节点)` ---- 删除指定的子节点

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			window.onload = function() {
				var btn1 = document.getElementById("btn1");
				btn1.onclick = function() {
					var yxlmNode = document.getElementById("yxlm");
					var gameNode = document.getElementById("game");

					gameNode.removeChild(yxlmNode);
				}

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
			<li id="yxlm">英雄联盟</li>
			<li>星际争霸</li>
			<li>魔兽世界</li>
		</ul>
		<button type="button" id="btn1">删除节点</button>
	</body>
</html>
~~~

### 确认提示信息

confirm(字符串) ---- 弹出一个确认框

当用户点击确认时返回true

当用户点击取消时，返回false

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			window.onload = function() {
				var btn1 = document.getElementById("btn1");
				btn1.onclick = function() {
					var yxlmNode = document.getElementById("yxlm");
					var gameNode = document.getElementById("game");

					var flag = confirm("确定删除" + yxlmNode.firstChild.NodeValue + "的元素消息吗？");

					if (flag) {
						gameNode.removeChild(yxlmNode);
					}
				}

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
			<li id="yxlm">英雄联盟</li>
			<li>星际争霸</li>
			<li>魔兽世界</li>
		</ul>
		<button type="button" id="btn1">删除节点</button>
	</body>
</html>

~~~

### parentNode

表示当前节点的父节点

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			window.onload = function() {
				var btn1 = document.getElementById("btn1");
				btn1.onclick = function() {
					var yxlmNode = document.getElementById("yxlm");
					var gameNode = document.getElementById("game");

					var myParent = yxlmNode.parentNode;
					var testNode = myParent.getElementsByTagName("li");
					alert(testNode[0].firstChild.nodeValue);
				}

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
			<li id="yxlm">英雄联盟</li>
			<li>星际争霸</li>
			<li>魔兽世界</li>
		</ul>
		<button type="button" id="btn1">删除节点</button>
	</body>
</html>
~~~

点谁删谁

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			window.onload = function() {

				var lis = document.getElementsByTagName("li");
				for (var i = 0; i < lis.length; i++) {
					lis[i].onclick = function() {
						if (confirm("确定删除" + this.firstChild.nodeValue + "节点吗？")) {
							this.parentNode.removeChild(this);
						}
					}
				}


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
			<li id="yxlm">英雄联盟</li>
			<li>星际争霸</li>
			<li>魔兽世界</li>
		</ul>
		<button type="button" id="btn1">删除节点</button>
	</body>
</html>

~~~

### 添加删除实例：员工管理系统

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<style type="text/css">
			body {
				text-align: center;
			}

			table {
				border-collapse: collapse;
				margin: 0px auto;
			}

			table,
			td,
			th {
				boder: 1px black solid;
				padding: 10px;
			}
		</style>

		<script type="text/javascript">
			function removeTr(aNode) {
				var trNode = aNode.parentNode.parentNode; // td  tr
				var nameText = trNode.getElementsByTagName("td")[0].firstChild.nodeValue;
				var flag = confirm("确定要删除：" + nameText + " 的信息吗？");
				if (flag) {
					trNode.parentNode.removeChild(trNode);
				}
			}

			window.onload = function() {
				//删除原始数据
				var aNodes = document.getElementsByTagName("a");
				for (var i = 0; i < aNodes.length; i++) {
					aNodes[i].onclick = function() {
						removeTr(this);
					}
				}


				//新增一条记录
				document.getElementById("btn1").onclick = function() {
					var trNode = document.createElement("tr");
					document.getElementById("table1").appendChild(trNode);

					for (var i = 0; i < 4; i++) {
						//前三个td
						if (i <= 2) {
							var textNode = document.createTextNode(document.getElementsByTagName("input")[i].value);
							var tdNode = document.createElement("td");
							trNode.appendChild(tdNode);

							tdNode.appendChild(textNode);
						} else {
							//最后一个特殊的td
							var textNode = document.createTextNode("Delete");
							var tdNode = document.createElement("td");
							trNode.appendChild(tdNode);
							var aNode = document.createElement("a");
							aNode.href = "#";
							tdNode.appendChild(aNode);
							aNode.appendChild(textNode);
							aNode.onclick = function() {
								removeTr(this);
							}
						}
					}
				}
			}
		</script>
	</head>
	<body>

		员工管理系统
		<br><br>
		name:<input type="text" name="" id="name" value="Lucy" />&nbsp;&nbsp;
		email:<input type="text" name="" id="email" value="Lucy@qq.com" />&nbsp;&nbsp;
		salary:<input type="text" name="" id="salary" value="10000" />&nbsp;&nbsp;

		<br><br>
		<button type="button" id="btn1">新增</button>
		<br><br>
		<hr>
		<br><br>
		<table border="" id="table1">
			<tr>
				<th>name</th>
				<th>email</th>
				<th>salary</th>
				<th></th>
			</tr>
			<tr>
				<td>Tom</td>
				<td>abc@qqcom</td>
				<td>8000</td>
				<td><a href="#">Delete</a></td>
			</tr>
			<tr>
				<td>Jerry</td>
				<td>abdfafc@qqcom</td>
				<td>80dd00</td>
				<td><a href="#">Delete</a></td>
			</tr>
			<tr>
				<td>Mary</td>
				<td>abdsfsfc@qqcom</td>
				<td>80031310</td>
				<td><a href="#">Delete</a></td>
			</tr>
		</table>
	</body>
</html>
~~~



### 元素节点隐藏显示

`元素节点.style.display=""`可以控制元素节点是否显示

- 取值为none表示隐藏
- 取值为list-item表示以列表项的形式展示
- 取值为block 表示以块级元素的形式展示

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			window.onload = function() {
				document.getElementById("btn1").onclick = function() {
					document.getElementById("yxlm").style.display = "none";
				}

				document.getElementById("btn2").onclick = function() {
					document.getElementById("yxlm").style.display = "list-item";
				}

				var flag = true;
				document.getElementById("btn3").onclick = function() {
					flag = !flag;
					if (flag) {
						document.getElementById("yxlm").style.display = "list-item";
					} else {
						document.getElementById("yxlm").style.display = "none";
					}

				}
			}
		</script>
	</head>
	<body>
		<input type="hidden" name="" id="" value="100" />


		<ul id="city">
			<li>北京</li>
			<li>上海</li>
			<li>广州</li>
			<li>南京</li>
		</ul>
		<br>
		<ul id="game">
			<li id="yxlm">英雄联盟</li>
			<li>星际争霸</li>
			<li>魔兽世界</li>
		</ul>
		<button type="button" id="btn1">隐藏英雄联盟</button>
		<button type="button" id="btn2">显示英雄联盟</button>
		<button type="button" id="btn3">显示/隐藏英雄联盟</button>
	</body>
</html>

~~~



### `<input type="hidden" value="xxx">` ---- 隐藏域

通常写在`<form>`中，他不显示，但会随着表单的提交而被提交

# js第三天

## 置灰

元素节点.disabled  属性表示是否置灰 ，它的取值为true和false，true表示置灰，false表示可用

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			window.onload = function() {
				document.getElementById("btn").onclick = function() {
					document.getElementById("t1").disabled = 										!document.getElementById("t1").disabled;
				}
			}
		</script>
		</script>
	</head>
	<body>

		<input type="text" name="" id="t1" value="" />
		<br>
		<button type="button" id="btn">置灰/取消置灰</button>
	</body>
</html>
~~~

## 只读

`元素节点.readOnly`  属性表示是否只读 ，它的取值为true和false，true表示只读，false表示可写

注意：disabled 和 readOnly 的本质区别在于disabled 中的value值无法随表单提交，而readOnly中的value值可以随表单提前交
~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			window.onload = function() {
				document.getElementById("btn").onclick = function() {
					document.getElementById("t1").readOnly = !document.getElementById("t1").readOnly;
				}
			}
		</script>
		</script>
	</head>
	<body>

		<input type="text" name="" id="t1" value="" />
		<br>
		<button type="button" id="btn">只读/可写</button>
	</body>
</html>
~~~

## innerHTML

它可以获取当前节点的HTML代码
也可以使用元素节点.innerHTML=新的HTML代码 来改变当前元素节点的子元素

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			window.onload = function() {
				document.getElementById("btn3").onclick = function() {
					var city = document.getElementById("city");
					alert(city.innerHTML);
				}

				document.getElementById("btn4").onclick = function() {
					var game = document.getElementById("game");
					alert(game.innerHTML);
				}

				document.getElementById("btn5").onclick = function() {
					var game = document.getElementById("game");
					var city = document.getElementById("city");
					var temp = city.innerHTML;
					city.innerHTML = game.innerHTML;
					game.innerHTML = temp;
				}

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
			<li id="yxlm">英雄联盟</li>
			<li>星际争霸</li>
			<li>魔兽世界</li>
		</ul>
		<br><br>
		<button type="button" id="btn3">获取city的html代码</button>
		<br><br>
		<button type="button" id="btn4">获取game的html代码</button>
		<br><br>
		<button type="button" id="btn5">交换</button>
	</body>
</html>

~~~

## 外部js文件

我们可以单独编写独立的js文件，然后再当前html中使用`<script type="text/javascript" src="外部js文件路径"/>`来将其引入 

~~~js
function abc() {
	alert("我是abc");
}
~~~

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="./myJs.js"></script>
		<script type="text/javascript">
			window.onload = function() {

				abc();

            }
		</script>
	</head>
	<body>
	</body>
</html>
~~~

## my97Date日期控件

一般来讲 日期框的内容都是用户手动选择的，而不是输入的。我们可以引入my97Date日期控件中的WdatePicker.js 然后再文本框的onclick事件上调用WdatePicker()即可，

当用户选择某日期后，返回的是该日期的标准格式字符串

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="My97DatePicker/WdatePicker.js"></script>

	</head>
	<body>
		<input type="text" onclick="WdatePicker()" />
	</body>
</html>
~~~

## jQuery

这是一个流行的封装了js的前端框架

窗体加载事件

~~~css
			$(function() {
				alert("hello jquery");
			})
~~~

### jQuery 的选择器

$("元素名") ---- 元素选择器，选中指定元素
$("#id值") ---- id选择器
$(".class值") --- class选择器
$("*") ---- 选中所有元素
注意：多个选择器可以同时选中，在$("，，，")中以逗号分割
$("[属性名]") ---- 属性选择器
$("[属性名=属性值]") ---- 含有指定属性值的属性选择器
注意 ： 
- != 表示没有该属性值
- ^=  表示以属性值开头  
- $=  表示以属性值结尾  
- *=  表示含有属性值


注意：多个选择器中间没有逗号，表示取其交集

注意：jQuery的选择器选择到的对象，其实是一个数组类型

注意：jQuery对象不能直接调用js的属性和方法，但它可以通过数组下标转型成js对象，然后就可以调用js属性和方法

$(":表单控件类型") ---- 表单选择器
$(":控件状态") ---- 表示选中指定状态的元素
注意：如果选择器中间有空格，那么表示在其子元素中进行相应的选择

在单选框指定的列表下添加数据：
~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="jquery-1.11.3.min.js"></script>
		<script type="text/javascript">
			$(function() {

				$("#sub").click(function() {
					var strValue = $("#str").val();
					strValue = $.trim(strValue);//取出两端空格
					if (strValue == null || strValue == "") {
						alert("请输入名称");
					} else {
						$("#" + $(":radio[name='type']:checked").val()).append($("<li> " + strValue + "</li>"));

					}
				})

			})
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
		<br>
		<p>请选择类型</p>
		城市<input type="radio" name="type" value="city" />
		游戏<input type="radio" name="type" checked="checked" value="game" />
		<br>
		<p>请输入名称</p>
		<input type="text" id="str" />
		<br><br>
		<button id="sub">提交</button>
	</body>
</html>
~~~

jQuery对象也可以通过get(下标)来转型js对象

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="jquery-1.11.3.min.js"></script>
		<script type="text/javascript">
			$(function() {
                //以下三种输出都一样
				var jsNode = $("p")[0];
				alert(jsNode.firstChild.nodeValue);
                
				alert($("p")[0].firstChild.nodeValue);
                
				alert($("p").get(0).firstChild.nodeValue);
			})
		</script>
	</head>
	<body>
		<p>我是一个段落</p>
		<br><br>
		<p>我是第二个段落</p>
		<br><br>
		<p>我是第三个段落</p>
	</body>
</html>

~~~

js对象也不能直接调用`jQuery`的方法，但是它可以先转型为`jQuery`对象

我们只需要使用`$(js对象)`，就可以实现js对象转`jQuery`对象

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="jquery-1.11.3.min.js"></script>
		<script type="text/javascript">
			$(function() {
				var p1Node = document.getElementById("p1");
				alert($(p1Node).text());
			})
		</script>
	</head>
	<body>
		<p id="p1">我是一个段落</p>
		<br><br>
		<p>我是第二个段落</p>
		<br><br>
		<p>我是第三个段落</p>
	</body>
</html>

~~~



### jQuery 的方法

#### text() 

---- 获取指定元素节点中的文本内容

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="jquery-1.11.3.min.js"></script>
		<script type="text/javascript">
			$(function() {

				alert($("#p1").text());
			})
		</script>
		</script>
	</head>
	<body>
		<p id="p1">我是一个段落</p>
	</body>
</html>
~~~

#### click() 

---- onClick事件

#### css(属性值，属性名) 

---- 改变元素节点的css样式

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="jquery-1.11.3.min.js"></script>
		<script type="text/javascript">
			$(function() {
				$("button").click(function() {
					$("#p1").css("color", "red");//单击按钮使第一个段落变成红色
				});
			})
		</script>
	</head>
	<body>
		<p id="p1">我是一个段落</p>
		<br><br>
		<p>我是第二个段落</p>
		<br><br>
		<p>我是第三个段落</p>
		<br>
		<button type="button">改变段落的颜色</button>
	</body>
</html>

~~~

#### change() 

---- onChange事件

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="jquery-1.11.3.min.js"></script>
		<script type="text/javascript">
			$(function() {
				$(".field1").change(function() {
					$(this).css("background-color", "red");
				})
			})
		</script>
	</head>
	<body>
		<input type="text" class="field1" />
		<br>
		<select class="field1">
			<option value="">北京</option>
			<option value="">上海</option>
			<option value="">广州</option>
			<option value="">深圳</option>
			<option value="">苏州</option>
		</select>
	</body>
</html>
~~~

#### mouseenter() 

---- onMouseenter事件

mouseleave() ---- onMouseleave事件

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="jquery-1.11.3.min.js"></script>
		<script type="text/javascript">
			$(function() {
				$("p").mouseenter(function() {
					$(this).css("background-color", "blue");
				})

				$("p").mouseleave(function() {
					$(this).css("background-color", "yellow");
				})
			})
		</script>
	</head>
	<body>
		<p id="p1">我是一个段落</p>
		<br><br>
		<p>我是第二个段落</p>
		<br><br>
		<p>我是第三个段落</p>
		<br>
		<button type="button">改变段落的颜色</button>
		<br>
		<input type="text" class="field1" />
		<br>
		<select class="field1">
			<option value="">北京</option>
			<option value="">上海</option>
			<option value="">广州</option>
			<option value="">深圳</option>
			<option value="">苏州</option>
		</select>
	</body>
</html>
~~~

#### hide() 

---- 隐藏指定元素节点

####  show() 

---- 显示隐藏的节点

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="jquery-1.11.3.min.js"></script>
		<script type="text/javascript">
			$(function() {
				$("p").click(function() {
					$(this).hide();
				})

				$("#btn1").click(function() {
					$("p").show();
				})

			})
		</script>
	</head>
	<body>
		<p id="p1">点我我就消失</p>
		<br><br>
		<p>俺也一样</p>
		<br><br>
		<p>俺也一样</p>
		<br>
		<button type="button" id="btn1">全部出现</button>
	</body>
</html>
~~~

#### is(":hidden") 

---- 判断当前控件是否隐藏，返回true和false

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="jquery-1.11.3.min.js"></script>
		<script type="text/javascript">
			$(function() {

				$("p").click(function() {
					$(this).hide();
				})
				$("#btn1").click(function() {
					$("p").show();
				})
				$("#btn2").click(function() {
					$("p").each(function() {
						alert($(this).is(":hidden"));
					})
				})
			})
		</script>
		</script>
	</head>
	<body>
		<p>点我我就消失</p>
		<p>点我我就消失2</p>
		<p>点我我就消失3</p>
		<button type="button" id="btn1">全部出来！</button>
		<button type="button" id="btn2">查看控件隐藏状态</button>
	</body>
</html>
~~~

#### find("元素节点") 

---- 在当前元素节点下的子节点中查找指定元素节点

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="jquery-1.11.3.min.js"></script>
		<script type="text/javascript">
			$(function() {


				$("#ul1").find("li").click(function() {
					$(this).hide();
				})

			})
		</script>
		</script>
	</head>
	<body>
		<ul id="ul1">
			<li>点我我就消失1</li>
			<li>点我我就消失2</li>
			<li>点我我就消失3</li>
		</ul>
		<ul id="ul2">
			<li>点我我不消失1</li>
			<li>点我我不消失2</li>
			<li>点我我不消失3</li>
		</ul>
	</body>
</html>

~~~
#### each() 

---- 遍历当前jQuery对象中的每一个元素节点

#### val()

---- 操作元素节点的value属性，如果无参，则是获取value值，如果传参数，则是改变value值

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="jquery-1.11.3.min.js"></script>
		<script type="text/javascript">
			$(function() {

				alert($("input").val());
				$("input").val("你好");
				alert($("input").val())
			})
		</script>
		</script>
	</head>
	<body>
		<input type="text" name="" id="" value="嗨嗨" />
	</body>
</html>
~~~

#### prop(属性名) 

---- 获取当前元素的某属性值

#### prop(属性名，新值)

---- 改变当前元素的某些属性

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="./jquery-1.11.3.min.js"></script>
		<script type="text/javascript">
			$(function() {
				var myValue = $("#test1").prop("value");
				alert(myValue);
				$("#test1").prop("value", "zhangsan");

			})
		</script>
	</head>
	<body>
		<input type="text" name="hello" id="test1" value="abc" title="haha" />
	</body>
</html>
~~~

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="./jquery-1.11.3.min.js"></script>
		<script type="text/javascript">
			$(function() {
				$("#btn1").click(function() {
					alert($("#c1").prop("checked"));
				})


				$("#btn2").click(function() {
					$("#c1").prop("checked", !$("#c1").prop("checked"))
				})
			})
		</script>
	</head>
	<body>
		<input type="text" name="hello" id="test1" value="abc" title="haha" />
		<br><br>
		<input type="checkbox" name="" id="c1" value="" />
		<button type="button" id="btn1">看看有没有选中</button>
		<br><br>
		<button type="button" id="btn2">选中</button>
	</body>
</html>
~~~

## 用jQuery写多选框
~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="jquery-1.11.3.min.js"></script>
		<script type="text/javascript">
			$(function() {

				$("#checkedAll").click(function() {
					$("[name='hobby']").prop("checked", this.checked);
				})


				$("[name='hobby']").click(function() {
					$("#checkedAll").prop("checked", $("[name=hobby]").length == $("[name=hobby]:checked").length);
				})

			})
		</script>
	</head>
	<body>


		<p>请选择你的爱好：</p>
		全选<input type="checkbox" id="checkedAll" />
		<br><br>
		足球<input type="checkbox" name="hobby" id="" value="football" />
		篮球<input type="checkbox" name="hobby" id="" value="basketball" />
		乒乓球<input type="checkbox" name="hobby" id="" value="pingpong" />
		羽毛球<input type="checkbox" name="hobby" id="" value="badminton" />
	</body>
</html>

~~~

### html() 

---- 可以获取指定元素节点下的子节点的html代码，如果传参，则是改变它的子节点的html代码，相当于innerHTML

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="jquery-1.11.3.min.js"></script>
		<script type="text/javascript">
			$(function() {

				$("#btn").click(function() {
					alert($("div").html());
					$("div").html("<h1>我是一个标题</h1>");
				})


			})
		</script>

	</head>
	<body>
		<div id="">
			<p>我是一个段落</p>
		</div>
		<button type="button" id="btn">按钮</button>
	</body>
</html>
~~~

### empty() 

---- 清空指定元素节点下的所有子节点

### remove() 

---- 删除指定元素节点以及它下面的所有字节点

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="jquery-1.11.3.min.js"></script>
		<script type="text/javascript">
			$(function() {

				$("#btn").click(function() {
					alert($("div").html());
					$("div").html("<h1>我是一个标题</h1>");
				})

				$("#btn2").click(function() {
					$("div").empty();
				})

				$("#btn3").click(function() {
					$("div").remove();
				})

			})
		</script>
		<style type="text/css">
			div {
				height: 80px;
				width: 80px;
				background-color: red;
			}
		</style>
	</head>
	<body>
		<div id="">
			<p>我是一个段落</p>
		</div>
		<button type="button" id="btn">按钮</button>
		<br>
		<button type="button" id="btn2">清空</button>
		<br>
		<button type="button" id="btn3">删除</button>
		<br>
	</body>
</html>
~~~

## 用 jQuery写点谁删谁

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="jquery-1.11.3.min.js"></script>
		<script type="text/javascript">
			$(function() {
				$("li").click(function() {
					if (confirm("确定删除" + $(this).text() + "的信息吗？")) {
						$(this).remove();
					}
				})
			})
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
			<li id="yxlm">英雄联盟</li>
			<li>星际争霸</li>
			<li>魔兽世界</li>
		</ul>
	</body>
</html>

~~~

### $(html代码字符串) 

---- 创建一个新的节点

### 将新节点挂在指定父节点下的最后一个位置的方法：

> 新节点.appendTo(父节点)
> 父节点.append(新节点)
~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="jquery-1.11.3.min.js"></script>
		<script type="text/javascript">
			$(function() {
				$("#btn1").click(function() {
					//$("<li>杭州</li>").appendTo($("#city"));
					$("#city").append($("<li>杭州</li>"));
				})

			})
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
			<li id="yxlm">英雄联盟</li>
			<li>星际争霸</li>
			<li>魔兽世界</li>
		</ul>
		<button type="button" id="btn1">新增一个城市</button>

	</body>
</html>
~~~

prependTo和prepend是挂在父节点的第一个子节点位置
insertBefore和before是挂在某个兄弟节点的前面
insertAfter和after是挂在某个兄弟节点的后面



### $.trim(字符串)
---- 去除字符串的前后空格



# js第四天
### parent() 
---- 找到指定节点的父节点

### find(元素名).eq(下标)
---- 找到指定元素数组的某个下标位置的元素
~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="jquery-1.11.3.min.js"></script>
		<script type="text/javascript">
			$(function() {
				$("#btn1").click(function() {
					//$("#id33").parent().parent().css("background-color","red");
					$("#id33").parent().parent().find("tr").eq(1).find("td").eq(1).css("background-color", "red");
				})
			})
		</script>
		<style type="text/css">

		</style>
	</head>
	<body>
		<table border="" cellspacing="" cellpadding="">
			<tr>
				<td>11</td>
				<td>12</td>
				<td>13</td>
			</tr>
			<tr>
				<td>21</td>
				<td>22</td>
				<td>23</td>
			</tr>
			<tr>
				<td>31</td>
				<td>32</td>
				<td id="id33">33</td>
			</tr>
		</table>
		<br>
		<button type="button" id="btn1">选中父标签的父标签</button>
	</body>
</html>
~~~



#### jQuery员工管理系统
~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<style type="text/css">
			body {
				text-align: center;
			}

			table {
				border-collapse: collapse;
				margin: 0px auto;
			}

			table,
			td,
			th {
				boder: 1px black solid;
				padding: 10px;
			}
		</style>
		<script type="text/javascript" src="jquery-1.11.3.min.js"></script>
		<script type="text/javascript">
			function removeTr(aNode) {
				//删除
				if (confirm("确定要删除：" + $(aNode).parent().parent().find("td").eq(0).text() + " 的信息吗"))
					$(aNode).parent().parent().remove();
			}
			$(function() {

				$("a").click(function() {
					removeTr(this);
				})

				//新增
				$("#btn1").click(function() {
					var trNode = $("<tr><td>" + $("#name").val() + "</td><td>" + $("#email").val() + "</td><td>" + $("#salary").val() + "</td><td><a href='#'>Delete</a></td></tr>");
					trNode.find("a").click(function() {
						removeTr(this);
					})
					$("#table1").append(trNode);
				})


			})
		</script>
	</head>
	<body>

		员工管理系统
		<br><br>
		name:<input type="text" name="" id="name" value="Lucy" />&nbsp;&nbsp;
		email:<input type="text" name="" id="email" value="Lucy@qq.com" />&nbsp;&nbsp;
		salary:<input type="text" name="" id="salary" value="10000" />&nbsp;&nbsp;

		<br><br>
		<button type="button" id="btn1">新增</button>
		<br><br>
		<hr>
		<br><br>
		<table border="" id="table1">
			<tr>
				<th>name</th>
				<th>email</th>
				<th>salary</th>
				<th></th>
			</tr>
			<tr>
				<td>Tom</td>
				<td>abc@qqcom</td>
				<td>8000</td>
				<td><a href="#">Delete</a></td>
			</tr>
			<tr>
				<td>Jerry</td>
				<td>abdfafc@qqcom</td>
				<td>80dd00</td>
				<td><a href="#">Delete</a></td>
			</tr>
			<tr>
				<td>Mary</td>
				<td>abdsfsfc@qqcom</td>
				<td>80031310</td>
				<td><a href="#">Delete</a></td>
			</tr>
		</table>
	</body>
</html>
~~~

## 正则表达式

用来校验某个字符串是否符合指定的规则

校验方法：
使用正则对象.test(字符串)  可以返回true 或者 false 表示校验是否通过

### 定义正则对象的语法：

1. 以/^ 开始  以 $/ 结尾
2. new RegExp("^正则表达式$");
~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="jquery-1.11.3.min.js"></script>
		<script type="text/javascript">
			$(function() {
				$("#btn1").click(function() {
					//var reg = /^a$/;
					var reg = new RegExp("^a$");
					alert(reg.test($("#str").val()));

				})
			})
		</script>
	</head>
	<body>
		<input type="text" name="" id="str" value="" />
		<br>
		<button type="button" id="btn1">校验</button>
	</body>
</html>
~~~

### 正则的语法
#### []
---- 在多个字符中进行选择匹配，满足其一（单个字符）即可
例：`new RegExp("^[ab]$")` //a b   都是true  ab却是 false
~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="jquery-1.11.3.min.js"></script>
		<script type="text/javascript">
			$(function() {
				$("#btn1").click(function() {
					//var reg = /^a$/;
					var reg = new RegExp("^[ab]$");
					alert(reg.test($("#str").val()));

				})
			})
		</script>
	</head>
	<body>
		<input type="text" name="" id="str" value="" />
		<br>
		<button type="button" id="btn1">校验</button>
	</body>
</html>
~~~
#### ^
---- 写在[]内表示取反
例：`new RegExp("^[^ab]$")` //a b ab  都是false
#### -
表示两个字符之间任意单个字符
例：`new RegExp("^[a-z]$")` 
注意：正则本身用到的特殊字符，如果要校验，得转义
注意：这些特殊字符如果在[]里面，那么无序转义，除了[]包[]，里面的[]仍需转义
使用  \  来转义
例：`var reg = /^\$$/;` // $ 为true
#### 元字符
小数点 ---- 除了换行符以外的任意单个字符
例：`var reg = /^.$/;`
\w ---- 任意单个字母数字下划线
例：`var reg = /^\w$/;`
\W ---- 任意单个 非 字母数字下划线 
例：`var reg = /^\W$/;`
\s ---- 单个空格
\S ---- 单个 非 空格
\d ---- 单个数字
\D ---- 单个 非 数字


# 问题

//只要有一个消失就会输出true  这输出的是哪一个？
~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="jquery-1.11.3.min.js"></script>
		<script type="text/javascript">
			$(function() {

				$("p").click(function() {
					$(this).hide();
				})
				$("#btn1").click(function() {
					$("p").show();
				})
				$("#btn2").click(function() {
					// $("p").each(function() {
					// 	alert($(this).is(":hidden"));
					// })
					alert($("p").is(":hidden"));
				})
			})
		</script>
		</script>
	</head>
	<body>
		<p>点我我就消失</p>
		<p>点我我就消失2</p>
		<p>点我我就消失3</p>
		<button type="button" id="btn1">全部出来！</button>
		<button type="button" id="btn2">查看控件隐藏状态</button>
	</body>
</html>

~~~

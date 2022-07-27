- **HTML ---- 超文本标记语言（毛坯）**
- **CSS ---- 层叠样式表（装潢）**
- **JavaScript ---- 页面脚本语言（布局）**

## HTML

### html结构

~~~~html
<html>标签是根标签，包含<head>和<body>
<head> </head>head部分是告诉浏览器如何展示内容
<body> </body>body部分是要展示的具体内容
   bgcolor属性 表示背景色
    我们可以使用 #六位十六进制数 表示一种颜色
    	前两位表示一种红
    	中间两位表示一种绿
    	后两位表示一种蓝
    	当前颜色就是它们叠加出来的颜色
    background属性表示背景图片的路径
<title> </title>表示浏览器选项卡上的标题
<h1></h1>到<h6></h6> 网页上的六级标题
<br/> 一个换行
&nbsp; 一个空格
<hr/> 换行并添加分割线
<P> </p> 表示一个段落
<a></a> 表示超链接，它的href属性表示目标页面的路径
    路径包括绝对路径和相对路径
    绝对路径：从根目录开始的路径<a href="绝对路径"></a>
    相对路径：从当前目录开始的路径
    			./ 表示在当前目录下寻找
    			../ 表示在当前目录的上层目录寻找
    			注意：./ 可以省略
<img> 图片，src属性表示某张图片的路径，路径可以是绝对或相对路径
    width表示图片的宽度，height表示图片的高度，单位是像素
<pre></pre> 保留代码中内容的原始格式
    
~~~~

~~~html
<table></table> 表示一个表格
	border属性表示边框的粗细，默认为0
	cellpadding属性表示内容和边框之间的距离
	cellspacing属性表示单元格之间的距离
<tr></tr>  <table></table>中的一行
<td></td> <tr></tr>中的一个单元格
<th></th> 表示表头，默认加粗和居中
	colspan="n" 表示跨n列
	rowspan属性表示跨行
	height属性表示高度
	width属性表示宽度
	align属性表示对齐方向
		left居左  right居右  center居中
<form></form> 表单，用于信息的录入，表单中有各种的表单控件
	action属性表示提交的目标路径
<input type="text"/> 文本框
<input type="password"/> 密码框
title属性表示鼠标旁边的提示信息
placeholder属性表示显示在控件中的提示信息
<input type="radio"/> 表示单选框
<input type="checkbox"/> 复选框
	name属性相同的为同一组
	checked="checked"表示默认选中
<select></select> 表示下拉框 里面包含若干<option></option>
	每个<option></option> 就是一个下拉选项
	注意：表单空间都包含value属性，表示“值”，随着表单提交传到后端的就是value值
<textarea></textarea> 文本域，可以用来输入一段文字
	rows和cols表示默认的宽度和高度
<input type="submit"/> 表示提交按钮
	value属性表示按钮上显示的文本内容
<input type="reset"/> 表示重置按钮，使得当前表单中所有内容恢复到默认状态
	value属性表示按钮上显示的文本内容
<input type="button" > 普通按钮
注意：<button></button> 在<form></form>之外 也表示普通按钮
~~~




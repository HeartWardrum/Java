# AngularJS

是一个JavaScript框架

通过以下script标签添加到网页中

~~~html
<script src="https://cdn.staticfile.org/angular.js/1.4.6/angular.min.js"></script>
~~~

**注意**：我们建议把脚本放在`<body>`元素的底部，这会提高网页加载速度，因为HTML加载不受制于脚本加载

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script src="https://cdn.staticfile.org/angular.js/1.4.6/angular.min.js"></script>
	</head>
	<body>
		
		
		<div ng-app="">
			<p>名字：<input type=" text" ng-model="name">
			</p>
			<h1>Hello {{name}}</h1>
			<P ng-bind="name"></P>
		</div>
		
		
	</body>
</html>
~~~

实例讲解：

当网页加载完毕，AngularJS自动开启。

ng-app指令告诉AngularJS，`<div>`元素是AngularJS应用程序的“所有者”

ng-model指令把输入域的值绑定到应用程序变量name

ng-bind指令把应用程序变量name绑定到某个段落的innerHTML



~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script src="https://cdn.staticfile.org/angular.js/1.4.6/angular.min.js"></script>

		<script>
			var app = angular.module('myApp',[]);
		app.controller('myCtrl',function($scope){
			$scope.firstName="John";
			$scope.lastName="Doe";
		});
	</script>

	</head>
	<body>


		<div ng-app="myApp" ng-controller="myCtrl">
			名：<input type="text" ng-model="firstName"><br>
			姓：<input type="text" ng-model="lastName"><br>
			<br>
			姓名：{{firstName + "  "  + lastName}}

		</div>

	</body>
</html>

~~~

这段HTML和JavaScript代码是一个简单的AngularJS示例，用于演示双向数据绑定。

让我解释一下：

1. **引入AngularJS库：**
   ```html
   <script src="https://cdn.staticfile.org/angular.js/1.4.6/angular.min.js"></script>
   ```
   这行代码引入了AngularJS库，使得你可以在页面中使用AngularJS框架。

2. **定义AngularJS应用和控制器：**
   ```javascript
   var app = angular.module('myApp',[]);
   app.controller('myCtrl',function($scope){
       $scope.firstName="John";
       $scope.lastName="Doe";
   });
   ```
   这里创建了一个名为`myApp`的AngularJS应用，并定义了一个控制器`myCtrl`。控制器中初始化了两个作用域变量`$scope.firstName`和`$scope.lastName`，分别表示名和姓。

3. **HTML部分：**
   ```html
   <div ng-app="myApp" ng-controller="myCtrl">
       名：<input type="text" ng-model="firstName"><br>
       姓：<input type="text" ng-model="lastName"><br>
       <br>
       姓名：{{firstName + "  "  + lastName}}
   </div>
   ```
   在HTML中，`ng-app`和`ng-controller`属性定义了AngularJS应用和控制器的作用范围。两个输入框通过`ng-model`与作用域中的变量进行双向数据绑定。最后一行使用插值表达式`{{ ... }}`来显示名和姓的组合。

总的来说，这个例子演示了AngularJS中的双向数据绑定，当输入框中的值发生变化时，显示的姓名也会相应地更新。
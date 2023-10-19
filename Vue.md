搭建Vue教程：[如何搭建一个vue项目(完整步骤)_vue项目搭建-CSDN博客](https://blog.csdn.net/weixin_44882488/article/details/124220864)

vue如何去除严格语法规范eslint：[【通俗易懂】vue如何去除严格语法规范eslint，用了vue-cli脚手架没有config文件怎么办_vue 语法严格_接口写好了吗的博客-CSDN博客](https://blog.csdn.net/seeeeeeeeeee/article/details/119418536)

## Vue

本地注册：

~~~vue
<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    // 可以在这里本地注册组件。
    HelloWorld,
  },
};
</script>
~~~

对于 `App.vue`，我们的默认导出将组件的名称设置为 `App` ，并通过将 `HelloWorld` 组件添加到 `components` 属性中来注册它。以这种方式注册组件时，就是在本地注册。本地注册的组件只能在注册它们的组件内部使用，因此你需要将其导入并注册到使用它们的每个组件文件中。

组件的 CSS 应该写在 `<style>` 标签里，如果你添加了 `scoped` 属性（形如 `<style scoped>`），Vue 会把样式的范围限制到单文件组件的内容里。这个是类似于 CSS-in-JS 的解决方案，只不过允许书写纯粹的 CSS。





1. 现在在你的组件模板中添加一个空的`<div>`。
2. 在那个 `<div>` 里面，让我们添加一个 `checkbox` 和一个对应的 `label`。给复选框添加一个 `id`，并添加一个 `for` 属性，将复选框映射到标签上，如下所示：

~~~vue
<template>
  <div>
    <input type="checkbox" id="todo-item" checked="false" />
    <label for="todo-item">My Todo Item</label>
  </div>
</template>
~~~



请注意，组件文件名及其在 JavaScript 中的表示方式总是用大写驼色（例如 `ToDoList`），而等价的自定义元素总是用连字符小写（例如 `<to-do-list>`）。



~~~vue
<script>
  export default {
    props: {
      label: { required: true, type: String },
      done: { default: false, type: Boolean }
    }
  };
</script>
~~~

label中：

1. 第一个 `required` 属性，它的值是 `true`. 这将会告诉 Vue 说，我们希望每个该组件的实例都必须有个 label 字段。如果 `ToDoItem` 组件没有 label 字段的话，Vue 会提示警告。
2. 第二是添加一个 `type` 属性。这个属性的值设为 JavaScript 的 `String` 类型。这等于告诉 Vue，我们希望 type 属性的值是 String 类型的。

done中：

1. 首先添加一个 `default` 属性，它的值是 `false`。这意味着当没有 `done` prop 被传递给 `ToDoItem` 组件时， `done` prop 的值会是 false（注意 default 属性不是必需的————我们只在非 required props 里才需要 `default` ）
2. 接着，添加一个 `type` 属性，值为 `Boolean`。这将告诉 Vue，我们希望这个 prop 的值是 JavaScript 的 Boolean 类型。
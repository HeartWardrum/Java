https://blog.csdn.net/qq_55754838/article/details/132237854



# 创建项目目录

一、使用脚手架搭件基础Vue框架
1、安装Node.js环境，打开终端命令界面，确保Node.js和npm已经安装。你可以在终端中运行以下命令来检查它们的版本：

```powershell
node -v
npm -v
```

2、安装Vue CLI：

```powershell
npm install -g @vue/cli
```

3、在终端进入你想创建的项目目录，用以下命令创建Vue项目：

```powershell
vue create 项目名称
```

然后选Vue3

4、创建完成后进入项目目录，并运行:

```powershell
cd 项目名称
npm run serve
```

现在，你可以在浏览器中访问http://localhost:8080来预览你的Vue应用程序。

# 安装element-plus

你在安装 `element-ui` 时遇到了依赖冲突的问题，这是因为 `element-ui` 是基于 Vue 2 的，而你的项目使用的是 Vue 3。为了在 Vue 3 项目中使用 `Element Plus`（专为 Vue 3 开发的 Element UI 版本），你需要安装 `element-plus` 而不是 `element-ui`。

请按照以下步骤解决这个问题：

1. **卸载可能的错误安装：**
   ```bash
   npm uninstall element-ui
   ```

2. **安装 Element Plus：**
   ```bash
   npm install element-plus
   ```

3. **在项目中引入 Element Plus：**
   在你的 Vue 项目入口文件（通常是 `main.js` 或 `main.ts`）中引入 Element Plus：
   ```javascript
   import { createApp } from 'vue';
   import App from './App.vue';
   import ElementPlus from 'element-plus';
   import 'element-plus/dist/index.css';
   
   const app = createApp(App);
   app.use(ElementPlus);
   app.mount('#app');
   ```

这应该能解决你在安装 Element UI 时遇到的依赖冲突问题。如果你还有其他问题或需要进一步的帮助，请告诉我。

# 向后端发送请求

https://blog.csdn.net/weixin_43275277/article/details/131778943
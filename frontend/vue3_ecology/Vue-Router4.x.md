<!--
 * @Author: zhangmaokai zmkfml@163.com
 * @Date: 2023-01-09 09:58:49
 * @LastEditors: zhangmaokai zmkfml@163.com
 * @LastEditTime: 2023-08-16 09:34:46
 * @FilePath: /记录/FullStacker/frontend/vue3_ecology/Vue-Router4.x.md
 * @Description: vue-router快速上手
-->

<img src="../../images/vue3/vue-router.png" style="zoom: 30%">

#### 🌟更详细的学习可以看着 [Vue-Router4.x](https://router.vuejs.org/zh/introduction.html)

因为vue是单页应用，不会有那么多html让我们跳转，所有要使用路由做页面的跳转。Vue 路由允许我们通过不同的 URL 访问不同的内容。通过 Vue 可以实现多视图的单页Web应用。

1. 先构建前端项目，看上方vite配置环境那一节，自己搭建一个router，不用脚手架生成的vue项目目录结构，这样会了解一些
```shell
# 注意vue3版本安装对应的router4版本
npm install vue-router@4
```
2. 在src目录下面新建router 文件 然后在router 文件夹下面新建 index.ts

```ts
/** src/router/index.ts */
//引入路由对象
import { createRouter, createWebHashHistory, createWebHistory, RouteRecordRaw } from "vue-router";

// 测试两个路由
const routers: Array<RouteRecordRaw> = [
  {
    path: "/",
    component: () => import('../components/Login.vue'), // 打包时 会进行代码分割 性能优化
  },
  {
    path: "/register",
    component: () => import('../components/Register.vue'), // 打包时 会进行代码分割 性能优化
  }
]

//vue2 mode history | vue3 createWebHistory
//vue2 mode  hash   | vue3  createWebHashHistory
//vue2 mode abstact | vue3  createMemoryHistory // SSR服务端渲染

const router = createRouter({
  history: createWebHashHistory(), 
  // history: createWebHistory(), 
  routes: routers
})

// 导出路由
export default router
```
路由模式：
 - **createWebHashHistory**: hash模式 基于hash实现 路由前面有'#/' 通过window.addEventListener('hashchange',(e)=>{console.log(e)}) 这个函数监听路由变化

 - **createWebHistory**: 基于history实现 路由前面没有'#/' 通过window.addEventListener('popstate',(e)=>{console.log(e)}) 监听路由变化
 
 - **createMemoryHistory** SSR服务端渲染

3. 通过router-view内置标签展示存放路由展示

```ts
<script setup lang="ts">
</script>

<template>
  <div>
    <span>vue3</span>
    <!-- router-view 路由出口 路由匹配到的组件将渲染在这里 -->
    <div>
      <router-link to="/" style="margin-right: 10px">登录</router-link>
      <router-link to="/register">注册</router-link>
    </div>
    <hr>
    <router-view></router-view>

  </div>
</template>

```
与此，还有一个router-link内置标签
请注意，我们没有使用常规的 a 标签，而是使用一个自定义组件 router-link 来创建链接。这使得 Vue Router 可以在不重新加载页面的情况下更改 URL，处理 URL 的生成以及编码。我们将在后面看到如何从这些功能中获益。

4. 最后在main.ts挂载
运行npm run dev启动项目即可点击查看路由跳转变化

```ts
import { createApp } from 'vue'
import './style.css'
import App from './App.vue'
import router from './router';

createApp(App)
  .use(router) // 挂载到main.ts中
  .mount('#app')
```


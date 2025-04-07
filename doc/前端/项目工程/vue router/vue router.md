# vue router

## 目录

- [安装](#安装)

Vue Router 是 [Vue.js](https://vuejs.org/ "Vue.js") 的官方路由。它与 Vue.js 核心深度集成，让用 Vue.js 构建单页应用变得轻而易举。功能包括：

- 嵌套路由映射
- 动态路由选择
- 模块化、基于组件的路由配置
- 路由参数、查询、通配符
- 展示由 Vue.js 的过渡系统提供的过渡效果
- 细致的导航控制
- 自动激活 CSS 类的链接
- HTML5 history 模式或 hash 模式
- 可定制的滚动行为
- URL 的正确编码

# 安装

```vue 
npm install vue-router@4
```


1. 创建router文件夹

```vue 
// index.ts
import {createRouter, createWebHashHistory, RouteRecordRaw} from 'vue-router'

const test = () => import('@/pages/test.vue')

// 2. 定义一些路由
// 每个路由都需要映射到一个组件。
const routes: Array<RouteRecordRaw> = [
    {
        path: '/login',
        name: 'login',
        meta: {
            title: '登录',
            hidden: true,
        },
        component: test,
    },
    {
        path: '/',
        component: test,
        meta: {
            title: '首页',
        },
        children: [
            {
                path: '',
                name: 'home',
                meta: {
                    title: '首页',
                    icon: 'homepage',
                },
                component: test,
            },
        ],
    },

]

// 3. 创建路由实例并传递 `routes` 配置
// 你可以在这里输入更多的配置，但我们在这里
const router = createRouter({
    // 4. 内部提供了 history 模式的实现。为了简单起见，我们在这里使用 hash 模式。
    history: createWebHashHistory(),
    routes: routes,
})

// 使用TS扩展
declare module 'vue-router' {
    interface RouteMeta {
        title: string;
        hidden?: boolean;
    }
}

// 导出router
export default router




```


全局守卫

```vue 
// permission.ts
import router from "@/router/index.ts";

// 全局前置守卫
router.beforeEach(async (to, from) => {
    console.log(to, from)
});

// 全局后置钩子
router.afterEach((to, from) => {
    // finish progress bar
    console.log(to, from)
});


```

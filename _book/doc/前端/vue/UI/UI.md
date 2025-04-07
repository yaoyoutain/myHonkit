# UI

## 目录

- [Element ](#Element-)
  - [安装](#安装)
  - [完整引入](#完整引入)
  - [volar支持](#volar支持)

# Element&#x20;

[ 一个 Vue 3 UI 框架 | Element Plus a Vue 3 based component library for designers and developers https://element-plus.gitee.io/zh-CN/](https://element-plus.gitee.io/zh-CN/ " 一个 Vue 3 UI 框架 | Element Plus a Vue 3 based component library for designers and developers https://element-plus.gitee.io/zh-CN/")

## 安装

```bash 

# npm 安装
npm install element-plus --save


```


## 完整引入

```bash 
// main.ts
import { createApp } from 'vue'
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'
import App from './App.vue'

const app = createApp(App)

app.use(ElementPlus)
app.mount('#app')
```


## volar支持

```bash 
// tsconfig.json
{
  "compilerOptions": {
    // ...
    "types": ["element-plus/global"]
  }
}
```

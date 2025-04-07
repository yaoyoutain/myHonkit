# pinia

## 目录

- [安装](#安装)
- [初步使用](#初步使用)
- [修改里面的值](#修改里面的值)
- [解构](#解构)
- [调用异步方法](#调用异步方法)
- [pinia 持久化](#pinia-持久化)
- [全部实例](#全部实例)

> 前言 全局状态管理工具

[Pinia](https://so.csdn.net/so/search?q=Pinia\&spm=1001.2101.3001.7020 "Pinia").js 有如下特点：

- 完整的 ts 的支持；
- 足够轻量，压缩后的体积只有1kb左右;
- 去除 mutations，只有 state，getters，actions；
- actions 支持同步和异步；
- 代码扁平化没有模块嵌套，只有 store 的概念，store 之间可以自由使用，每一个store都是独立的
- 无需手动添加 store，store 一旦创建便会自动添加；
- 支持Vue3 和 Vue2

[ Pinia 🍍 Intuitive, type safe, light and flexible Store for Vue https://pinia.vuejs.org/](https://pinia.vuejs.org/ " Pinia 🍍 Intuitive, type safe, light and flexible Store for Vue https://pinia.vuejs.org/")

## 安装

npm install pinia&#x20;

npm i pinia-plugin-persistedstate

```vue 
# main.ts
import { createPinia } from 'pinia';
import persist from 'pinia-plugin-persistedstate'

// 引用pinia
let pinia = createPinia()
pinia.use(persist)
app.use(pinia)

```


## 初步使用

```vue 
//store-nameSpace
export const enum Names {
    test = 'test'
}

// ts
import { useTestStore } from '../../store/test';
// 使用pinia
const test = useTestStore()


//temp
pinia :{{ test.curren }}名称：{{ test.name }}

//store ts
import { defineStore } from 'pinia';
import { Names } from './store-nameSpace';



export const useTestStore = defineStore(Names.test, {
    // 初始化值
    state: () => {
        return {
            curren: 100,
            name: "小满"
        }
    },
    // 格式化： 类似于computed 
    getters: {
    
    },
    //类似于methods 可以操作异步，同步提交
    actions: {
        setCurren() {
            this.curren++
        },
        setName(n: string) {
            this.name = n
        }
    }

})



```


## 修改里面的值

```vue 
// 修改pinia
// 1.test.curren++
// 2.test.$patch({    curren: 88, name: "Ceshi"    })
// 3.test.$patch((state) => {    state.curren = state.curren + 1        state.name = 'ceshi'    })
// 4.全部替换   test.$state = {        curren: 1,        name: 'ces'    }
// 5.test.setCurren()  ,test.setName("测试")
```


## 解构

```vue 
//ts
import { storeToRefs } from 'pinia';

// pinia  解构是不具有响应式
// const { curren, name } = test
// 需要包裹一层storeToRefs
const { curren, name } = storeToRefs(test)

```


## 调用异步方法

```vue 
//store ts actions
 async setInit() {
            this.user = await Login()
       },
       
       
const Login = (): Promise<user> => {
    return new Promise((resolve) => {
        setTimeout(() => {
            resolve({
                name: "飞机",
                age: 18
            })
        }, 2000)

    })
}

```


## pinia 持久化

```vue 
//main.ts
import { createPinia } from 'pinia'
import persist from 'pinia-plugin-persistedstate'

let pinia = createPinia()
pinia.use(persist)
app.use(pinia)


// store
export const useTestStore = defineStore(Names.test, {
    // 初始化值
    state: () => {
        return {
           name: "小满"
        }
    },
    persist:true,
    //类似于methods 可以操作异步，同步提交
    actions: {
        async setInit() {
            this.user = await Login()
        },
    }

})



```


## 全部实例

> store ts

```vue 
//store ts
import { defineStore } from 'pinia';
import { Names } from './store-nameSpace';

type user = {
    name: string
    age: number
}

const Login = (): Promise<user> => {
    return new Promise((resolve) => {
        setTimeout(() => {
            resolve({
                name: "飞机",
                age: 18
            })
        }, 2000)

    })
}

export const useTestStore = defineStore(Names.test, {
    // 初始化值
    state: () => {
        return {
            user: <user>{},
            curren: 100,
            name: "小满"
        }
    },
    // 格式化： 类似于computed 
    getters: {
        getUser(): string {
            let age = this.getAge
            return `名称=${this.user.name},年龄=${age}`
        },
        getAge(): number {
            return this.user.age
        }

    },
    //类似于methods 可以操作异步，同步提交
    actions: {
        async setInit() {
            this.user = await Login()
        },
        setCurren() {
            this.curren++
        },
        setName(n: string) {
            this.name = n
        }
    }

})




```


> home.vue

```vue 
<template>
    <div>
        pinia :{{ test.curren }}名称：{{ test.name }}
        <br>
        解构 :{{ curren }}名称：{{ name }}
        <button @click="change">change</button>
        <button @click="asyncInit">asyncInit</button>
        <br>
        异步:{{ test.user }}
        <br>
        格式化:{{ test.getUser }}
    </div>
</template>

<script setup lang="ts">
import { useTestStore } from '../../store/test';
import { storeToRefs } from 'pinia';


// 使用pinia
const test = useTestStore()

// pinia  解构是不具有响应式
// const { curren, name } = test
// 需要包裹一层storeToRefs
const { curren, name } = storeToRefs(test)
console.log('test=======>', test);

// 修改pinia
// 1.test.curren++
// 2.test.$patch({    curren: 88, name: "Ceshi"    })
// 3.test.$patch((state) => {    state.curren = state.curren + 1        state.name = 'ceshi'    })
// 4.全部替换   test.$state = {        curren: 1,        name: 'ces'    }
// 5.test.setCurren()  ,test.setName("测试")

const change = () => {
    test.setCurren()
    test.setName("测试")
}

const asyncInit = () => {
    test.setInit()
}


</script>
<style scoped lang="less"></style>
```

# 依赖注入provide inject

## 目录

- [传递](#传递)
- [接收](#接收)
  - [代码](#代码)
    - [home](#home)
    - [A](#A)
    - [B](#B)

> 父组件向子组件传递数据

# 传递

provide('key', color)  //子组件可以修改

provide('key', readonly(color))  //传递只读

# 接收

let color = inject\<Ref\<string>>('key')     //根据传递的key 接收

## 代码

### home

```vue 
<template>
  <div>
    <br>
    这个是home
    <label for="redColor">
      <input type="radio" name="core" v-model="color" value="red" id="redColor">红色
    </label>
    <label for="greenColor">
      <input type="radio" name="core" v-model="color" value="green" id="greenColor">绿色
    </label>
    <label for="gainsboroColor">
      <input type="radio" name="core" v-model="color" value="gainsboro" id="gainsboroColor">白色
    </label>
    <div class="box">

    </div>
    <hr>
    <IndexA></IndexA>
    <IndexB></IndexB>
  </div>
</template>

<script setup lang="ts">
import { ref, provide, readonly } from 'vue'
import IndexA from './IndexA.vue'
import IndexB from './IndexB.vue'

let color = ref<string>("red")
provide('color', readonly(color))

</script>

<style scoped>
.box {
  height: 200px;
  width: 100%;
  background-color: v-bind(color);
}
</style>
```


### A

```vue 
<template>
  <div> 我是A
    <button @click="change">修改颜色</button>
    <div class="box">

    </div>
  </div>
</template>

<script setup lang="ts">
import { inject, ref } from 'vue';
import { Ref } from 'vue';

let color = inject<Ref<string>>('color')

const change = () => {
  color!.value = "yellow"
}
</script>

<style scoped>
.box {
  height: 200px;
  width: 100%;
  background-color: v-bind(color);
}
</style>
```


### B

```vue 
<template>
  <div>
    我是B
    <div class="box">

    </div>
  </div>
</template>

<script setup lang="ts">
import { inject, ref } from 'vue';
import { Ref } from 'vue';

let color = inject<Ref<string>>('color')
</script>

<style scoped>
.box {
  height: 200px;
  width: 100%;
  background-color: v-bind(color);
}
</style>
```

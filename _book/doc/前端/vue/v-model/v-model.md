# v-model

> 可以绑定表单， 自定义组件， input , select &#x20;
> 在vue3中是破坏性更新的，v-model 其实是一个语法糖由props和emit组合而成的&#x20;

- prop：`value` -> `modelValue`；
- 事件：`input` -> `update:modelValue`；
- `v-bind` 的 `.sync` 修饰符和组件的 `model` 选项已移除
- 新增 支持多个v-model
- 新增 支持自定义 修饰符 Modifiers

子组件

```vue 
<template>
    <div v-if="modelValue" class="model">
        <div class="close"><button @click="close">关闭</button></div>
        <h3>我是v-model子组件</h3>
        <div>内容：<input @input="change" type="text" :value="textVal"></div>
    </div>
</template>

<script setup lang="ts">
let props = defineProps<{
    modelValue: boolean
    // 多个v-modle绑定
    textVal: string
    //  接收自定义修饰器必须要绑定name+Modifiers
    textValModifiers?: {
        isBt: boolean
    }
}>()

// 定义回发事件
// 必须要update:加v-model绑定的name 这样才会绑定到val的ref的对象上
let emit = defineEmits<{
    (e: "update:modelValue", flag: boolean): void
    (e: "update:textVal", string: string): void
}>()

const close = () => {
    // 回发
    emit("update:modelValue", false)
}
const change = (e: Event) => {
    // 回发
    let target = e.target as HTMLInputElement
    let str = props.textValModifiers?.isBt ? target.value + "变态" : target.value

    emit("update:textVal", str)
}
</script>

<style>
.model {
    width: 500px;
    height: 300px;
    border: 1px solid #ccc;
    position: fixed;
}
</style>
```


父组件

```vue 
<template>
    <div>
        我是home父组件
        <br>
        flag:{{ flag }}
        textVal:{{ text }}
        <button @click="flag = !flag">开关</button>
        <Index v-model:textVal.isBt="text" v-model="flag"></Index>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import Index from './Index.vue';

let flag = ref<boolean>(true)
let text = ref<string>("我是友田")
</script>

<style></style>
```

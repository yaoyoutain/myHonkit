# 自定义hook

## 目录

- [官方](#官方)
- [自定义](#自定义)

> 其实就是一个函数

&#x20;

# 官方

> import { useAttrs, useSlots } from 'vue';

# 自定义

> 我们引用hooks 时候， 我们需要单个单个引入，index文件他会帮我们自动拼接好&#x20;

```vue 
<template>
    <div>
        <img id="img" width="600" height="600" src="../../assets/img/Capture001.png" alt="这是一个图片">
    </div>
    <hr>
    <div>
        num1:<input v-model.number="num1" style="width:100px" />
        <br />
        num2:<input v-model.number="num2" style="width:100px" />
    </div>
    <span>加法等于:{{ addNum }}</span>
    <br />
    <span>减法等于:{{ subNum }}</span>
</template>


<script setup lang="ts">
import { ref } from 'vue';

import useBase64 from '../../Hooks/useBase64';
import useAdd from '../../Hooks/useAdd';
import useSub from '../../Hooks/useSub';

let num1 = ref(2)
let num2 = ref(1)
let { addNum, addFunc } = useAdd(num1, num2)
let { subNum, subFunc } = useSub(num1, num2)

addFunc(num1.value, num2.value)
subFunc(num1.value, num2.value)

useBase64({
    el: "#img"
}).then(res => {
    console.log('res :>> ', res.baseUrl);
})

</script>


<style></style>
```


ts文件

```vue 
import { ref, watch } from 'vue';
import type { Ref } from 'vue';

const useAdd = (num1: Ref<number>, num2: Ref<number>) => {
    let addNum = ref(0)
    watch([num1, num2], ([num1, num2]) => {
        addFunc(num1, num2)
    })
    const addFunc = (num1: number, num2: number) => {
        addNum.value = num1 + num2
    }

    return {
        addNum, addFunc
    }
}

export default useAdd
```

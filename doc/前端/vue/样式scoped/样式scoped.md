# 样式scoped

[scoped](https://so.csdn.net/so/search?q=scoped\&spm=1001.2101.3001.7020 "scoped")的原理

vue中的scoped 通过在DOM结构以及css样式上加唯一不重复的标记:data-v-hash的方式，以保证唯一（而这个工作是由过PostCSS转译实现的），达到样式私有化模块化的目的。

总结一下scoped三条渲染规则：

1. 给HTML的DOM节点加一个不重复data属性(形如：data-v-123)来表示他的唯一性
2. 在每句css选择器的末尾（编译后的生成的css语句）加一个当前组件的data属性选择器（如\[data-v-123]）来私有化样式
3. 如果组件内部包含有其他组件，只会给其他组件的最外层标签加上当前组件的data属性

PostCSS会给一个组件中的所有dom添加了一个独一无二的动态属性data-v-xxxx，然后，给CSS选

Vue 提供了样式穿透:deep() 他的作用就是用来改变 属性选择器的位置

```vue 
<template>
    <div>
        <el-input placeholder="测试代码" class="dmain" />
    </div>
</template>

<script lang="ts" setup>
</script>

<style scoped lang="less">
// .dmain[data-v-0330b3b4]
.dmain {
    width: 200px;
    height: 200px;

    // .dmain[data-v-0330b3b4]
    // 样式穿透，可以命中
    :deep(input) {
        background: red;
    }

    // 不加样式穿透， 不可以命中 
    // input {
    //     background: red;
    // }
}
</style>
```

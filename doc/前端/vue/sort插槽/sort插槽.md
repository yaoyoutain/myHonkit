# sort插槽

## 目录

- [子组件](#子组件)
- [父组件](#父组件)

插槽就是子组件中的提供给父组件使用的一个[占位符](https://so.csdn.net/so/search?q=占位符\&spm=1001.2101.3001.7020 "占位符")，用\<slot>\</slot> 表示，父组件可以在这个占位符中填充任何模板代码，如 HTML、组件等，填充的内容会替换子组件的\<slot>\</slot>标签。

## 子组件

```vue 
<template>
    <div>
        <br>
        <slot></slot>
        <br>
        <slot name="content"></slot>
        <br>
        <hr>
        <slot name="foot"></slot>
    </div>
</template>
```


## 父组件

```vue 
<SoltA>
            <!-- 插槽简单使用 -->
            <template v-slot>
                12323
            </template>
            <!-- 插槽有名称 -->
            <template v-slot:content>
                这里是内容
            </template>
            <!-- 插槽简写 -->
            <template #foot>
                这里是尾部
            </template>
        </SoltA>
```

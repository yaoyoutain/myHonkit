# svg

```bash title="安装"
npm i vite-plugin-svg-icons -D
```


```vue title="vite.config.ts"

import {createSvgIconsPlugin} from "vite-plugin-svg-icons";
import path from 'path';

export default defineConfig({
    plugins: [
    ...,
    createSvgIconsPlugin({
            // 指定需要缓存的图标文件夹
            iconDirs: [path.resolve(process.cwd(), 'src/icons/svg')],
            // 指定symbolId格式
            symbolId: '[name]',
        }),
    ]
})
```


```vue title="src/main.ts"
import 'virtual:svg-icons-register'
```


```vue title="src/components/SvgIcon.vue"
<script setup lang="ts">
import {computed} from 'vue';

const props = withDefaults(
    defineProps<{
      iconName: string; // svg图标名称
      width?: number;// 宽
      height?: number;// 高
      color?: string; // 填充颜色
    }>(),
    {
      width: 20,
      height: 20,
      color: '#000000',
    }
)

// 获取svg图标名称，需要和vite.config.ts中的配置保持一致
const iconName = computed(() => `#${props.iconName}`);

</script>

<template>
  <svg aria-hidden="true" :width="width" :height="height">
    <use :href="iconName" :fill="color" />
  </svg>
</template>

<style scoped>

</style>
```

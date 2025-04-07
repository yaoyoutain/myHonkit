# vite @ 别名

```vue 
// 先按照node包
npm i @types/node

// vite.config.ts


import {resolve} from 'node:path'

export default defineConfig({
   // 设置别名
    resolve: {
        alias: {
            "@": resolve(__dirname, "./src"),
            "@layout": resolve(__dirname, "./src/layout"),
        }
    }
})


// tsconfig.json配置
// {
//     "compilerOptions": {
//     ///...
//     // 配置别名
//     "baseUrl": ".",
//         "paths": {
//         "@/*": [
//             "src/*"
//         ],
//             "@layout/*": [
//             "src/layout/*"
//         ]
//     }
// }
// }



```

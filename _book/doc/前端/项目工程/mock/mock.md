# mock

npm i -d mockjs

npm install --save-dev @types/mockjs

```vue 
// src/mock/index.ts

import Mock, {Random} from 'mockjs'

let baseUrl = import.meta.env.VITE_APP_HTTP + import.meta.env.VITE_APP_HTTP_PREFIX
// 这里一定要加上监听的地址和端口
Mock.mock(baseUrl + '/ping', "get", {
    code: 200,
    'data|1-10': [
        {
            "id|+1": 1,
            "name": Random.name(),
        }
    ]
})



```


```vue 
// src/main.ts
import "@/mock"
```

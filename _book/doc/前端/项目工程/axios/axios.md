# axios

[ 起步 | Axios 中文文档 | Axios 中文网  https://www.axios-http.cn/docs/intro](https://www.axios-http.cn/docs/intro " 起步 | Axios 中文文档 | Axios 中文网  https://www.axios-http.cn/docs/intro")

安装： npm install axios

```vue 
// src/http/index.ts
import axios from 'axios'
import {decodeErrorCode, decodeErrorStatus} from "./tool.ts";

// 创建axios实列
const instance = axios.create({
    baseURL: import.meta.env.VITE_APP_HTTP + import.meta.env.VITE_APP_HTTP_PREFIX, // 域名配置
    timeout: 1000 * 5, //超时配置
    responseType: 'json',
    withCredentials: true,
})

// 添加请求拦截器
// 开始请求时，之前的操作
instance.interceptors.request.use(function (config) {
    // 判断是否登录
    return config
}, function (error) {
    // 对请求错误做些什么
    return Promise.reject(error)
})

// 添加响应拦截器
instance.interceptors.response.use(function (response) {
    // 判断是否登录
    let {status, data} = response

    if (status == 200) {
        return data
    }

    return data
}, function (error) {
    let message = ''
    let {code, response} = error

    // 判断有无返回体
    if (response) {
        const {status} = response
        if (status === 401) {
            // 跳回登录
            return
        }

        message = decodeErrorStatus(status)
    } else {
        message = decodeErrorCode(code)
    }

    if (message === "") {
        return Promise.reject(error)
    } else {
        return Promise.reject(new Error(message))
    }
})

export default instance
```


```vue 
// src/http/tool.ts
const ERR_FR_TOO_MANY_REDIRECTS = "ERR_FR_TOO_MANY_REDIRECTS";
const ERR_BAD_OPTION_VALUE = "ERR_BAD_OPTION_VALUE";
const ERR_BAD_OPTION = "ERR_BAD_OPTION";
const ERR_NETWORK = "ERR_NETWORK";
const ERR_DEPRECATED = "ERR_DEPRECATED";
const ERR_BAD_RESPONSE = "ERR_BAD_RESPONSE";
const ERR_BAD_REQUEST = "ERR_BAD_REQUEST";
const ERR_NOT_SUPPORT = "ERR_NOT_SUPPORT";
const ERR_INVALID_URL = "ERR_INVALID_URL";
const ERR_CANCELED = "ERR_CANCELED";
const ECONNABORTED = "ECONNABORTED";
const ETIMEDOUT = "ETIMEDOUT";

export const decodeErrorCode = (code: string) => {
    let message = ""
    switch (code) {
        case ERR_FR_TOO_MANY_REDIRECTS:
            message = '过多的重定向'
            break
        case ERR_BAD_OPTION_VALUE:
            message = '错误选项值'
            break
        case ERR_BAD_OPTION:
            message = '错误选项'
            break
        case ERR_NETWORK:
            message = '连接失败'
            break
        case ERR_DEPRECATED:
            message = "弃用"
            break
        case ERR_BAD_RESPONSE:
            message = '错误的返回结果'
            break
        case ERR_BAD_REQUEST:
            message = '错误的请求'
            break
        case ERR_NOT_SUPPORT:
            message = '不支持'
            break
        case ERR_INVALID_URL:
            message = '无效的url'
            break
        case ERR_CANCELED:
            message = '取消'
            break
        case ECONNABORTED:
            message = '远程主机拒绝网络服务'
            break
        case ETIMEDOUT:
            message = '结束'
            break
        default:
            message = code
    }

    return message
}

export const decodeErrorStatus = (status: number) => {
    let message = ""
    switch (status) {
        case 302:
            message = '接口重定向了！'
            break
        case 400:
            message = '参数不正确！'
            break
        case 401:
            message = '您未登录，或者登录已经超时，请先登录！'
            break
        case 403:
            message = '您没有权限操作！'
            break
        case 404:
            message = `请求地址出错`
            break
        case 408:
            message = '请求超时！'
            break
        case 409:
            message = '系统已存在相同数据！'
            break
        case 500:
            message = '服务器内部错误！'
            break
        case 501:
            message = '服务未实现！'
            break
        case 502:
            message = '网关错误！'
            break
        case 503:
            message = '服务不可用！'
            break
        case 504:
            message = '服务暂时无法访问，请稍后再试！'
            break
        case 505:
            message = 'HTTP 版本不受支持！'
            break
        default:
            message = ""
            break
    }

    return message
}



```

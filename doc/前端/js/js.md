# js

## 目录

- [入门](#入门)
  - [入口函数](#入口函数)
- [js的数据类型](#js的数据类型)
  - [查看数据类型](#查看数据类型)
  - [类型转换](#类型转换)
  - [字符串](#字符串)
  - [数组](#数组)
  - [对象](#对象)
- [函数](#函数)
- [js 选择器](#js-选择器)
- [事件](#事件)
- [dom操作](#dom操作)
  - [节点关系](#节点关系)
  - [节点操作方法](#节点操作方法)
- [dom 操作html ](#dom-操作html-)
- [dom操作css](#dom操作css)
- [dom 中表单与属性操作](#dom-中表单与属性操作)
- [属性操作](#属性操作)
- [其他](#其他)
  - [时间](#时间)
  - [json](#json)

[ 原生 JavaScript 教程 - 长乐未央  https://clwy.cn/guide/documents/javascript-clwy](https://clwy.cn/guide/documents/javascript-clwy " 原生 JavaScript 教程 - 长乐未央  https://clwy.cn/guide/documents/javascript-clwy")

# 入门

## 入口函数

```javascript
// 当所有文件都已经加载完毕
<script>
    window.onload = function(){
        //其他代码放在这里
    }
</script>

// 按照顺序加载
<script>
     function welcome(){
       alert('欢迎光临长乐未央~');
     }
</script>

```

# js的数据类型

1. 字符串string
2. 数字 number&#x20;
3. 布尔 Boolean
4. 空 null
5. 未定义 undefined
6. 符号

## 查看数据类型

```javascript
// 字符串
var txt = "欢迎光临";
console.log(typeof txt);
```

## 类型转换

```javascript
// 转字符串
string(变量)

//转数字
parseInt()
//转浮点
parseFloat()
```

## 字符串

| 属性或方法      | 意义                              |
| --------------- | --------------------------------- |
| length `属性` | 长度                              |
| charAt          | 所在位置的字符串                  |
| charCodeAt      | 所在位置字符串的字符编码          |
| concat          | 拼接多个字符，实际常用 `+` 拼接 |
| slice           | 截取                              |
| substr          | 截取                              |
| substring       | 截取                              |
| indexOf         | 字符串所在索引位置                |
| lastIndexOf     | 从后向前搜索字符串，找到索引位置  |
| trim            | 去除空格                          |
| toLowerCase     | 转小写                            |
| toUpperCase     | 转大写                            |
| split           | 字符串分割成数组                  |

## 数组

```javascript
var cars = ["Saab", "Volvo", "BMW"];
```

| 方法                 | 意义                        |
| -------------------- | --------------------------- |
| join                 | 数组连接成字符串            |
| push                 | 从后面推入                  |
| unshift              | 从前面推入                  |
| pop                  | 取得并删除最后一项          |
| shift                | 取得并删除第一项            |
| reverse              | 反转                        |
| sort                 | 排序                        |
| concat               | 连接数组                    |
| slice                | 将数组的一部分复制成新数组  |
| splice               | 修改数组 (删除、修改、新增) |
| indexOf、lastIndexOf | 取得索引值                  |
| forEach              | 遍历数组                    |
| map                  | 遍历并返回新数组            |
|                      |                             |

## 对象

> 创建

```javascript
// 1. 声明对象
var obj = {}
// 2. 构造函数创建
var x = new Object()

```

> 定义

```javascript
// 1
var person = {
    name: '刘备',
    age: 29
}

// 2
var person  = new Object();
person.name = '刘备';
person.age = 29;


```

# 函数

```javascript
// 定义函数
function hello(x) {
  return "hello world"+x;
}

//执行
hello(); //我就是开关

```

# js 选择器

| 代码                            | 意义                                                |
| ------------------------------- | --------------------------------------------------- |
| document.getElementsByTagName   | 标签选择器                                          |
| document.getElementById         | ID 选择器                                           |
| document.getElementsByClassName | Class 选择器                                        |
| document.getElementsByName      | 选取带有指定 name 属性的元素 (不常用)               |
| document.querySelector          | HTML5 中新加入的，接受一个 CSS 选择符，只匹配第一个 |
| document.querySelectorAll       | HTML5 中新加入的， 匹配所有元素                     |

# 事件

| 事件                | 意义                               |
| ------------------- | ---------------------------------- |
| onclick             | 鼠标单击                           |
| ondblclick          | 鼠标双击                           |
| onkeyup             | 按下并释放键盘上的一个键时触发     |
| onchange            | 文本内容或下拉菜单中的选项发生改变 |
| onfocus             | 获得焦点，表示文本框等获得鼠标光标 |
| onblur              | 失去焦点                           |
| onmouseover         | 鼠标悬停                           |
| onmouseout          | 鼠标移出                           |
| onload              | 网页文档加载事件                   |
| onunload            | 关闭网页时                         |
| onsubmit            | 表单提交事件                       |
| onreset             | 重置表单时                         |
| e.stopPropagation() | 阻止事件冒泡                       |

```javascript
// 添加点击事件
btn.addEventListener("click", getMaxByTreeNum);
```

# dom操作

| 方法           | 意义         |
| -------------- | ------------ |
| createElement  | 创建元素节点 |
| createTextNode | 创建文本节点 |

## 节点关系

| 方法                   | 意义                                                             |
| ---------------------- | ---------------------------------------------------------------- |
| children               | 子元素节点，不包含换行等                                         |
| childNodes             | 子节点，包含文本、换行等                                         |
| parentNode             | 父节点，注意是单数                                               |
| previousSibling        | 前一个同辈节点，包括文本节点、注释节点即回车、换行、空格、文本等 |
| previousElementSibling | 前一个同辈节点，不包括文本节点、注释节点                         |
| nextSibling            | 后一个同辈节点，包括文本节点、注释节点即回车、换行、空格、文本等 |
| nextElementSibling     | 后一个同辈节点，不包括文本节点、注释节点等                       |
| firstChild             | 第一个子节点，包含文本                                           |
| firstElementChild      | 第一个子节点，不包含文本                                         |
| lastChild              | 最后一个子节点，包含文本                                         |
| lastElementChild       | 最后一个子节点，不包含文本                                       |

## 节点操作方法

| 方法           | 意义                                                                              |
| -------------- | --------------------------------------------------------------------------------- |
| appendChild()  | 在最后面追加                                                                      |
| insertBefore() | 参数 1: 要插入的节点 参数 2: 作为参照的节点，如果为 null，与 appendChild 效果相同 |
| replaceChild() | 替换节点 参数 1: 要插入的节点 参数 2: 要替换的节点                                |
| removeChild()  | 移除节点 参数: 要移除的节点                                                       |
| cloneNode()    | 复制节点 参数（可选）：true，克隆时包含子元素                                     |

# dom 操作html&#x20;

| 方法                                     | 意义                      |
| ---------------------------------------- | ------------------------- |
| innerHTML                                | 修改元素内部 HTML         |
| outerHTML                                | 获取、修改整个元素的 HTML |
| innerText                                | 修改元素内部文本          |
| outerText                                | 获取、修改整个元素的文本  |
| insertAdjacentHTML(插入位置， html 内容) | 插入新的 html             |

# dom操作css

> dom中有个集合：classList

```javascript
<script>
    var demo = document.getElementById("demo");
    console.log(demo.classList);

    // 新增class
    demo.classList.add('ghost');

    // 删除class
    demo.classList.remove('big');
 
     // 切换class
    demo.classList.toggle('blue');

    // 是否包含class
    console.log(demo.classList.contains('blue'));
</script>
```

# dom 中表单与属性操作

```javascript
<input type="text" id="username" value="aaron" >
<script>
  var username = document.getElementById("username");
  
  // 取值
  console.log(username.value);
  // 设置值
  user.value = "pipi";
</script>

```

# 属性操作

| 方法            | 意义     |
| --------------- | -------- |
| getAttribute    | 得到属性 |
| setAttribute    | 设置属性 |
| removeAttribute | 移除属性 |

# 其他

## 时间

| 方法                 | 意义                                                     |
| -------------------- | -------------------------------------------------------- |
| Date()               | 返回当日的日期和时间。                                   |
| getDate()            | 从 Date 对象返回一个月中的某一天 (1\~ 31)。              |
| getDay()             | 从 Date 对象返回一周中的某一天 (0\~ 6)。                 |
| getMonth()           | 从 Date 对象返回月份 (0\~ 11)。                          |
| getFullYear()        | 从 Date 对象以四位数字返回年份。                         |
| getYear()            | 请使用 getFullYear() 方法代替。                          |
| getHours()           | 返回 Date 对象的小时 (0\~ 23)。                          |
| getMinutes()         | 返回 Date 对象的分钟 (0\~ 59)。                          |
| getSeconds()         | 返回 Date 对象的秒数 (0\~ 59)。                          |
| getMilliseconds()    | 返回 Date 对象的毫秒 (0\~ 999)。                         |
| getTime()            | 返回 1970 年 1 月 1 日至今的毫秒数。                     |
| getTimezoneOffset()  | 返回本地时间与格林威治标准时间 (GMT) 的分钟差。          |
| getUTCDate()         | 根据世界时从 Date 对象返回月中的一天 (1\~ 31)。          |
| getUTCDay()          | 根据世界时从 Date 对象返回周中的一天 (0\~ 6)。           |
| getUTCMonth()        | 根据世界时从 Date 对象返回月份 (0\~ 11)。                |
| getUTCFullYear()     | 根据世界时从 Date 对象返回四位数的年份。                 |
| getUTCHours()        | 根据世界时返回 Date 对象的小时 (0\~ 23)。                |
| getUTCMinutes()      | 根据世界时返回 Date 对象的分钟 (0\~ 59)。                |
| getUTCSeconds()      | 根据世界时返回 Date 对象的秒钟 (0\~ 59)。                |
| getUTCMilliseconds() | 根据世界时返回 Date 对象的毫秒 (0\~ 999)。               |
| parse()              | 返回 1970 年 1 月 1 日午夜到指定日期（字符串）的毫秒数。 |
| setDate()            | 设置 Date 对象中月的某一天 (1\~ 31)。                    |
| setMonth()           | 设置 Date 对象中月份 (0\~ 11)。                          |
| setFullYear()        | 设置 Date 对象中的年份（四位数字）。                     |
| setYear()            | 请使用 setFullYear() 方法代替。                          |
| setHours()           | 设置 Date 对象中的小时 (0\~ 23)。                        |
| setMinutes()         | 设置 Date 对象中的分钟 (0\~ 59)。                        |
| setSeconds()         | 设置 Date 对象中的秒钟 (0\~ 59)。                        |
| setMilliseconds()    | 设置 Date 对象中的毫秒 (0\~ 999)。                       |
| setTime()            | 以毫秒设置 Date 对象。                                   |
| setUTCDate()         | 根据世界时设置 Date 对象中月份的一天 (1\~ 31)。          |
| setUTCMonth()        | 根据世界时设置 Date 对象中的月份 (0\~ 11)。              |
| setUTCFullYear()     | 根据世界时设置 Date 对象中的年份（四位数字）。           |
| setUTCHours()        | 根据世界时设置 Date 对象中的小时 (0\~ 23)。              |
| setUTCMinutes()      | 根据世界时设置 Date 对象中的分钟 (0\~ 59)。              |
| setUTCSeconds()      | 根据世界时设置 Date 对象中的秒钟 (0\~ 59)。              |
| setUTCMilliseconds() | 根据世界时设置 Date 对象中的毫秒 (0\~ 999)。             |
| toSource()           | 返回该对象的源代码。                                     |
| toString()           | 把 Date 对象转换为字符串。                               |
| toTimeString()       | 把 Date 对象的时间部分转换为字符串。                     |
| toDateString()       | 把 Date 对象的日期部分转换为字符串。                     |
| toGMTString()        | 请使用 toUTCString() 方法代替。                          |
| toUTCString()        | 根据世界时，把 Date 对象转换为字符串。                   |
| toLocaleString()     | 根据本地时间格式，把 Date 对象转换为字符串。             |
| toLocaleTimeString() | 根据本地时间格式，把 Date 对象的时间部分转换为字符串。   |
| toLocaleDateString() | 根据本地时间格式，把 Date 对象的日期部分转换为字符串。   |
| UTC()                | 根据世界时返回 1970 年 1 月 1 日 到指定日期的毫秒数。    |
| valueOf()            | 返回 Date 对象的原始值。                                 |

## json

| 函数                                                                                      | 描述                                           |
| ----------------------------------------------------------------------------------------- | ---------------------------------------------- |
| [JSON.parse()](https://www.runoob.com/js/javascript-json-parse.html "JSON.parse()")             | 用于将一个 JSON 字符串转换为 JavaScript 对象。 |
| [JSON.stringify()](https://www.runoob.com/js/javascript-json-stringify.html "JSON.stringify()") | 用于将 JavaScript 值转换为 JSON 字符串。       |

## js 执行机制

### 同步任务

> 从上到下

### 异步任务

#### 宏任务

> script(整体代码)、setTimeout、setInterval、UI交互事件、postMessage、Ajax

#### 微任务

Promise.then catch finally、MutaionObserver、process.nextTick(Node.js 环境)

所有的同步任务都是在主进程执行的形成一个执行栈，主线程之外，还存在一个"任务队列"，

异步任务执行队列中先执行宏任务，然后清空当次宏任务中的所有微任务，

然后进行下一个tick如此形成循环。

### NextTaick

创建一个异步任务 。&#x20;

```vue 
<template>
    <div ref="div">{{ inputA }}</div>
    <input type="button" @click="change" :value="inputA">
</template>
<script setup lang="ts">
import { ref, nextTick } from 'vue';

let inputA = ref<string>("测试")
let div = ref<HTMLDivElement>()
const change = async () => {
    inputA.value = "测试ADS"
    await nextTick()
    // 没有await nexTick ：测试
    // 测试ADS
    console.log(div.value?.innerText);
}

</script>
<style scoped lang="less"></style>
```
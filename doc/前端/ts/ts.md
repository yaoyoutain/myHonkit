# ts
[toc]

## 入门&#x20;

```bash 
# 安装ts
npm install typescript -g

```

## 类型

### 变量声明

> let valName :(type)=val

### 基础类型(type)&#x20;

TS是JS的超集，所以JS基础的类型都包含在内&#x20;

&#x20;\| 来支持多种类型

1. any： 任意类型
2. string  ：字符串  ( \` \` ) 可以用来嵌套文本和表达式
3. number ： 数字 双精度 64 位浮点值
4. boolean ： 布尔
5. \[] 数组类型： number\[]，Array\<number>&#x20;
6. 元组： 也是数组的一种， 只不过里面的各个元素类型可能不同  let x: \[string, number]
7. enum ： 枚举 ，enum Color {Red, Green, Blue};
8. void ：空
9. null ： 空
10. undefined ： 用于初始化变量为一个未定义的值
11. never ：其它类型（包括 null 和 undefined）的子类型，代表从不会出现的值。

### 注意：

### void 和 undefined 和 null 最大的区别

> 与 `void` 的区别是，`undefined` 和 `null` 是所有类型的子类型。

### 任意类型

1. any  : 类似与c# 中的T : 没有限制哪种类型
2. unknown ： 顶级类型， &#x20;

#### any

1. 弊端如果使用any 就失去了TS类型检测的作用
2. 没有限制哪种类型

#### unknown&#x20;

1. 不能调用属性和方法
2. 所有类型都可以分配给它

### 接口

> 类似于结构体
> 关键字**interface**（接口）
> 使用**interface**来定义一种约束，让数据的结构满足约束的格式

```typescript 
//定义接口
interface person extends B{
  readonly id :number,
  name string,
  age? number,
  [propName:string]any,
  cb:()=>{
    console.log(123)
  }
}

interface B{
  xxx:string
}

//定义函数
interface Fn{
  (name:string):number[]
}

const fn:Fn=(name:string)=>{
  return [1]
}

```


1. 接口重名会自动重合
2. 任意key
3. ？，readonly
4. 接口继承 extends
5. 定义函数类型

##### 注：

1. 使用接口约束的时候不能多一个属性也不能少一个属性
2. 必须与接口保持一致

### 数组类型

> 在类型后面 加上中括号&#x20;

let valName :(type\[])=val&#x20;

1. 泛型数组： Array\<number>
2. arguments 类数组

#### arguments类数组

```typescript 

function Arr(...args:any): void {
    console.log(arguments) 
    //ts内置对象IArguments 定义
    let arr:IArguments = arguments
}
Arr(111, 222, 333)
 
//其中 IArguments 是 TypeScript 中定义好了的类型，它实际上就是：
interface IArguments {
  [index: number]: any;
  length: number;
  callee: Function;
}
```


### 类型断言

类型断言可以用来手动指定一个值的类型，即允许变量从一种类型更改为另一种类型。

值 as 类型


## 函数

## number 对象方法

| 方法               | 解释                                                      |
| ---------------- | ------------------------------------------------------- |
| toFixed()        | 把数字转换为字符串，并对小数点指定位数。                                    |
| toLocaleString() | 把数字转换为字符串，使用本地数字格式顺序。                                   |
| toPrecision()    | 把数字格式化为指定的长度。                                           |
| toString()       | 把数字转换为字符串，使用指定的基数。数字的基数是 2 \~ 36 之间的整数。若省略该参数，则使用基数 10。 |
| valueOf()        | 返回一个 Number 对象的原始数字值。                                   |


## string 对象方法

### 属性

| length    | 返回字符串的长度。      |
| --------- | -------------- |
| prototype | 允许您向对象添加属性和方法。 |

### 方法

| charAt()            | 返回在指定位置的字符。                                   |
| ------------------- | --------------------------------------------- |
| charCodeAt()        | 返回在指定的位置的字符的 Unicode 编码。                      |
| concat()            | 连接两个或更多字符串，并返回新的字符串。                          |
| indexOf()           | 返回某个指定的字符串值在字符串中首次出现的位置。                      |
| lastIndexOf()       | 从后向前搜索字符串，并从起始位置（0）开始计算返回字符串最后出现的位置。          |
| localeCompare()     | 用本地特定的顺序来比较两个字符串                              |
| match()             | 查找找到一个或多个正则表达式的匹配。                            |
| replace()           | 替换与正则表达式匹配的子串                                 |
| search()            | 检索与正则表达式相匹配的值                                 |
| slice()             | 提取字符串的片断，并在新的字符串中返回被提取的部分                     |
| split()             | 把字符串分割为子字符串数组。                                |
| substr()            | 从起始索引号提取字符串中指定数目的字符。                          |
| substring()         | 提取字符串中两个指定的索引号之间的字符。                          |
| toLocaleLowerCase() | 根据主机的语言环境把字符串转换为小写，只有几种语言（如土耳其语）具有地方特有的大小写映射。 |
| toLocaleUpperCase() | 据主机的语言环境把字符串转换为大写，只有几种语言（如土耳其语）具有地方特有的大小写映射。  |
| toLowerCase()       | 把字符串转换为小写。                                    |
| toString()          | 返回字符串。                                        |
| valueOf()           | 返回指定字符串对象的原始值。                                |
| toUpperCase()       | 把字符串转换为大写。                                    |


## 数组

| concat()      | 连接两个或更多的数组，并返回结果。                                  |
| ------------- | -------------------------------------------------- |
| every()       | 检测数值元素的每个元素是否都符合条件。                                |
| filter()      | 检测数值元素，并返回符合条件所有元素的数组。                             |
| forEach()     | 数组每个元素都执行一次回调函数。                                   |
| indexOf()     | 搜索数组中的元素，并返回它所在的位置。&#xA;&#xA;如果搜索不到，返回值 -1，代表没有此项。 |
| join()        | 把数组的所有元素放入一个字符串。                                   |
| lastIndexOf() | 返回一个指定的字符串值最后出现的位置，在一个字符串中的指定位置从后向前搜索。             |
| map()         | 通过指定函数处理数组的每个元素，并返回处理后的数组。                         |
| pop()         | 删除数组的最后一个元素并返回删除的元素。                               |
| push()        | 向数组的末尾添加一个或更多元素，并返回新的长度。                           |
| reduce()      | 将数组元素计算为一个值（从左到右）。                                 |
| reduceRight() | 将数组元素计算为一个值（从右到左）。                                 |
| reverse()     | 反转数组的元素顺序。                                         |
| shift()       | 删除并返回数组的第一个元素。                                     |
| slice()       | 选取数组的的一部分，并返回一个新数组。                                |
| some()        | 检测数组元素中是否有元素符合指定条件                                 |
| sort()        | 对数组的元素进行排序。                                        |
| splice()      | 从数组中添加或删除元素。                                       |
| toString()    | 把数组转换为字符串，并返回结果。                                   |
| unshift()     | 向数组的开头添加一个或更多元素，并返回新的长度。                           |


## 接口

```vue 
interface interface_name { 
}
```


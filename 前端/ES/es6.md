# ES6回顾学习
> [参考链接](https://zhuanlan.zhihu.com/p/87699079)

## 开始
1. ES与JavaScript关系?
> ES 全称ECMAScript，是通过ECMA-262标准化的脚本程序设计语言。它是一个语言标准，所以不局限js，描述了：语法、类型、语句、关键字、保留字、操作符、全局对象。

>JS 全称JavaScript,具有函数轻量级、解释型或即时编译的编程语言（脚本语言），JavaScript 实现了ECMAScript，它包括：核心（ECMAScript）、文档对象模型（DOM）、浏览器对象模型（BOM）

>TS 全称TypeScript,是微软开发的一个开源的编程语言，通过在JavaScript的基础上添加静态类型定义构建而成。TypeScript通过TypeScript编译器或Babel转译为JavaScript代码。他是JS的超集

2. ES6？
> ES6是ECMA为JavaScript制定的第6个标准版本，ECMAscript 2015是在2015年6月发布ES6的第一个版本。以此类推，ECMAscript 2016是ES6的第二个版本。ES6既是一个历史名词也是一个泛指，含义是5.1版本以后的JavaScript下一代标准，目前涵盖了ES2015、ES2016、ES2017、ES2018、ES2019、ES2020

3. 内容  
+ 声明let、const
> let const没有变量提升，只能在代码块执行.
+ 解构赋值 
> 解构将右边的非对象和数组数据转为对象，再解构赋值

> + 字符串解构： const [a,b,c,d,e] = "hello"  </br>
> + 数值解构： const {toString :s } =123; ===>const {toString:c } = new Number(123);  
>  toString:s 解构中的重命名(因为对象的解构，属性名必须相同),相当于 const {toString} =new Number(123); const s = toString;  
>  解构默认值生效条件：属性值严格等于undefine</br>
> + 布尔解构： const {toString :b} =true;同数值解构 </br>
> + 对象解构:默认：const { x, y = 2 } = { x: 1 } </br> 改名：const { x, y: z } = { x: 1, y: 2 }
> + 数组解构：默认值：const [x,y=3] = [1,2]
> + 函数参数解构，同上面解构
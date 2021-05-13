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

4. 字符串
   > 从ES2015开始，字符串字面量又称模板字面  

   > 基本字符串分为字符串字面量（通过单引号或者双引号定义）和String方法（不是new）获得.调用方法时，自动将字面量转为对象
    
   + 普通可打印字符
   + 特殊字符，需要添加转义字符 
   
    |  code | \0  | \\  |\n| \r |\t | \f |
    |---    |---   |---   |---   |---   |---   |
    | ouput | 空字符  |反斜杠  |回车  |水平制表符 |换页  |

    tips:
    + 长代码可以使用+连接，也可以在行末尾添加\ 表示继续
    +  eval() 函数可计算某个字符串，并执行其中的的 JavaScript 代码。eval字面量会执行代码，eval字符串对象会当对象处理
  函数
  + charAt(index) 获取某个字符 || string[index]
  + charCodeAt()  返回指定索引的字符的Unicode的值。   
  +  字符串比较 > < 
  +  endsWith() ，是否以给定字符串结尾，返回boolean ||startWith
  +  includes() 是否包含指定字符串。
  +  indexOf 返回首次发现给定值的索引
  +  lastIndexOf() 返回最后一个
  +  match(arg) 使用正则表达式或字符串比较，返回捕获组array---拓展
  +  padEnd(length,string) 用一个字符串填充当前字符串（需要的话，会重复）。返回到达指定长度的字符串
  +  padStart() 从字符串左侧开始填充
  +  repeat(count) 返回一个指定重复次数连接的字符串
  +  replace(arg) 被用来在正则表达式和字符串直接比较，然后用新的子串来替换被匹配的子串。  --拓展
  +  search(arg) 执行正则表达式或者字符串和 string的匹配，返回第一个匹配项的起始下标
  +  slice(start,end) 提取字符串的一部分，返回新字符串（不改动源字符串)，不包括end索引的字符
  +  split(string，limit) ,string不写返回原字符串，空字符串则返回按字符分割，limit表示限定返回分割片段数量，到达数目时，停止返回
  +  substr() 避免使用，要废弃,被shustring替代
  +  substring(start，end) 返回开始索引到结束索引的字符串子集，end不包括在内，length>index>0
  +  toLocaleLowerCase() toLocaleUpperCase()，toLowerCase() toUpperCase全大写或全小写
  +   trim() 去空格（只能去除首尾两端的空格）  trimStart() trimEnd()
  +   其他转string ，优先String(),而不是toString，如null
  
  5. 数值
   + 二进制表示 0b或者0B，八进制 0o或者0O
   + Number.EPSILON最小精度
   + Number.MIN_SAFE_INTEGER:最小安全数值（-2^53）,MAX 2^53
   + Number.parseInt()取整，拿到整数部分
   + Number.parseFloat() 取浮点数，1.2222=> 1.222
   + Number.isFinite ，是否为有限数值
   + Number.isInteger 是否为整数
   + Number.isSafeInteger 是否在安全数值范围之内
   + Math.trunc 返回数值整数部分（可使用字符串--只包含数字，包括其他则NAN）
   + Math.sign 返回符号 1，-1 0
   + Math.cbrt 立方根
   + Math.imul（number1，number2）转为32 位整数相乘。
   + Math.fround 指定数字最接近的32位单精度
   + Math.hypot(...args) 函数返回所有参数的平方和的平方根
   + Math.expm1()：返回e^n - 1

   6. 对象
      + Object.is()：对比两值是否相等
      +  Object.assign(target, ...sources)：合并对象(浅拷贝)，返回目标对象 ，只能获取一层
      + Object.getPrototypeOf()：返回对象的原型对象
      + Object.setPrototypeOf()：设置对象的原型对象
      + for-in：遍历对象自身可继承可枚举属性，得到属性
      + Object.keys()：返回对象自身可枚举属性键组成的数组，得到属性
      + Object.getOwnPropertyNames()：返回对象自身非Symbol属性键组成的数组
      + Object.getOwnPropertySymbols()：返回对象自身Symbol属性键组成的数组
   7. 数组
       + Array.from()：转换具有Iterator接口的数据结构为真正数组
       + Array.of()：转换一组值为真正数组
       + copyWithin(placeIndex,start,end--不包括)：浅复制数组的一部分到同一数组中的另一个位（该位置被替换），返回原数组
       + keys()：返回以索引值为遍历器的对象
       + values()：返回以属性值为遍历器的对象
       + entries()：返回以索引值和属性值为遍历器的对象
    8. 函数
       + rest/spread； spread 表示展开语法，使用中表示为...，rest为数组，表示剩余参数
       + 箭头函数无自己的this
       + name返回函数名
 正则表达式
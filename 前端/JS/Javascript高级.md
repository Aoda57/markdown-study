# Javascript高级

[学习来源](https://www.bilibili.com/video/BV1Wb411H7Pj?p=2)

## 基础总结
### 基础数据类型
+ 基本(值)类型
  + Numbuer、String、Boolean、null、undefined
+ 对象(引用)类型
  + Object、Array、Function(特殊的对象--可执行)、Date
  + Set(es6) 、Map(es6)
  + 特殊的基本包装类型(String、Number、Boolean)
#### 判断
+ typeof ：基础类型的判断 function object ，无法判断null，得通过===
+ instanceof ：对象的具体类型判断
+ === （全等，不做数据转化  ）或者 ==

#### TIPS
+ undefined vs null 
  > undefined表示值定义，未赋值。null表示定义且赋值了，但是值为null
  > null 使用在将要赋值为对象，但还不知道对象是多少 或者赋值null，来让js垃圾回收机制回收赋值的对象
+ 数据类型 vs 变量类型
  > 数据类型: 基本类型、对象类型
  > 变量（变量内存值的类型）类型: 基本类型、引用
  类型

### 对象
> 多个数据的封装体 || 保持多个数据的容器 

### 函数

+ 执行方式
  + test() 直接调用
  + obj.test() 对象调用
  + new test() 
  + test.call(obj) 

### 回调函数
> 用户自定义、用户未调用、函数执行

### IIFE 
> Imemediately-Invoked Function Expression
> 立即执行函数表达式
> 用来编码js模块

``` javascript
(function (){
  console.log("1");

})()
```

作用
+ 隐藏实现
+ 不会污染外部命名空间
+ 便于代码压缩

### 原型对象/显示原型  prototype 
> 每个函数都有prototype属性,默认指向空的Object实例对象（原型对象）
> 原型对象中的constructor指向函数，定义函数时添加
> 每个实例对象也有一个__proto__,称为隐式对象，创建实例对象时添加
> 作用：函数的所有实例对象自动拥有原型上的方法和属性
> 隐式原型的值等于显示原型的值


tips：
+ 程序员只能操作显式原型属性（prototype），不能操作隐式原型（__proto__）----ES6之前
+ prototype 函数独有，__proto__ 和constructor对象独有，因为函数也是对象，所以函数具有__proto__ 和prototype
+ Object 函数的prototype属性 =》Object.prototype.__proto__ ===null
+ 所有函数都是Funtion的实例，包括他自身


### 原型链
> 别名 ：隐式原型链，作用：<strong>查找</strong>对象的属性
> 
> 访问一个对象的属性，查找流程，先在自身属性查找 -> 沿__proto__去寻找 -> 未找到 返回undefined

tips:
+ 如果给对象设置属性，不沿着原型链寻找，直接在当前对象上设置属性


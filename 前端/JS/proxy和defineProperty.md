




# Proxy
[参考](https://es6.ruanyifeng.com/#docs/proxy)
Proxy 用于修改默写操作的默认行为.可以理解成在目标对象之前架设一层拦截，外界对该对象的访问，必须先通过这层拦截。单词翻译为代理，表示用他来代理某些操作

1. Proxy 支持的拦截操作共13种
+ get(target,propKey,receiver)  ,receiver代表原始的读操作所在的那个对象,一般情况下就是 Proxy 实例。
  
+ set(target ,propKey,value,receiver)
  
+ has(target,propKey) 拦截 propKey in Proxy 操作 ，has()方法拦截的是HasProperty操作，而不是HasOwnProperty操作，即has()方法不判断一个属性是对象自身的属性，还是继承的属性。<strong>对for in 循环操作无效</strong>
  
+ deleteProperty(target,propKey) 拦截delete proxy[propKey]操作，返回bool

+ apply(target, object, args)：拦截 Proxy 实例作为函数调用的操作，比如proxy(...args)、proxy.call(object, ...args)、proxy.apply(...),参数分别为目标对象、目标对象的上下文对象（this）和目标对象的参数数组。
  
+ construct(target, args)：拦截 Proxy 实例作为构造函数调用的操作，比如new proxy(...args)。用于拦截new命令
+ 
+  defineProperty(target, propKey, propDesc)：拦截Object.defineProperty(proxy, propKey, propDesc）、Object.defineProperties(proxy, propDescs)，返回一个布尔值
  
+ ownKeys(target)：拦截Object.getOwnPropertyNames(proxy)、Object.getOwnPropertySymbols(proxy)、Object.keys(proxy)、for...in循环，返回一个数组。该方法返回目标对象所有自身的属性的属性名，而Object.keys()的返回结果仅包括目标对象自身的可遍历属性。
  
+  getOwnPropertyDescriptor(target, propKey)：拦截Object.getOwnPropertyDescriptor(proxy, propKey)，返回属性的描述对象。
  
+ preventExtensions(target)：拦截Object.preventExtensions(proxy)，返回一个布尔值。
  
+ getPrototypeOf(target)：拦截Object.getPrototypeOf(proxy)，返回一个对象。
  
+ isExtensible(target)：拦截Object.isExtensible(proxy)，返回一个布尔值
  
+ setPrototypeOf(target, proto)：拦截Object.setPrototypeOf(proxy, proto)，返回一个布尔值。如果目标对象是函数，那么还有两种额外操作可以拦截。
  
2. 中断代理
Proxy 支持随时取消对 target 的代理，这一操作常用于完全封闭对数据或接口的访问。在下面的示例中，我们使用了 Proxy.revocable 方法创建了可撤销代理的代理对象：
一旦某个代理对象被撤销，它将变得几乎完全不可调用，在它身上执行任何的可代理操作都会抛出 异常.此外一旦被撤销，这个代理对象便不可能被直接恢复到原来的状态，同时和它关联的目标对象以及处理器对象都有可能被垃圾回收掉。再次调用撤销方法 revoke() 则不会有任何效果，但也不会报错。
```javascript
const proxy = new Proxy(target,handler)

var revocable = Proxy.revocable({}, {
  get(target, name) {
    return "[[" + name + "]]";
  }
});
var proxy = revocable.proxy;
proxy.foo;              // "[[foo]]"

// 取消拦截
revocable.revoke();
//或者写法 Proxy.revoke(proxy,handler)

console.log(proxy.foo); // 抛出 TypeError
proxy.foo = 1           // 还是 TypeError
delete proxy.foo;       // 又是 TypeError
typeof proxy            // "object"，因为 typeof 不属于可代理操作
```


# defineProperty
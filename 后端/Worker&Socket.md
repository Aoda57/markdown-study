# Web Worker
[阮一峰](http://www.ruanyifeng.com/blog/2018/07/web-worker.html)  
[MDN worker API](https://developer.mozilla.org/zh-CN/docs/Web/API/Web_Workers_API)   
[worker同源限制](https://paper.seebug.org/57/)

> Worker就是为JS创造多线程环境。JS是单线程的，处理一些复杂、耗时的操作，容易造成堵塞或者看起来失去响应。Worker可以创建一个线程，独立于JS运行的主线程，分担这些复杂耗时的任务。   
> Worker 线程一旦新建成功，就会始终运行，不会被主线程上的活动（比如用户点击按钮、提交表单）打断。这样有利于随时响应主线程的通信。但是，这也造成了 Worker 比较耗费资源，不应该过度使用，而且一旦使用完毕，就应该关闭.
## 使用
### 主线程
1. 主线程创建：
   ``` javascript
        worker=new Worker('worker.js')
   ```
> Worker()构造函数，可以接受两个参数。第一个参数是脚本的网址（必须遵守同源政策），该参数是必需的，且只能加载 JS 脚本，否则会报错。第二个参数是配置对象，该对象可选。它的一个作用就是指定 Worker 的名称，用来区分多个 Worker 线程。
2. 主线程接受子线程消息：
    ``` javascript
        worker.onmessage=function(event){
            console.log(event.data)
        }
   ```
3. 主线程与子线程通信：
      ``` javascript
      var data;
        worker.postMessage(data)
   ```
### 子线程
1. 子线程即worker.js内容。子线程的self为子线程的全局对象，即子线程自身。
> Web Worker 有自己的全局对象，不是主线程的window，而是一个专门为 Worker 定制的全局对象。因此定义在window上面的对象和方法不是全部都可以使用。
Worker 线程有一些自己的全局属性和方法。  
self.name： Worker 的名字。该属性只读，由构造函数指定。   
self.onmessage：指定message事件的监听函数。  
self.onmessageerror：指定 messageerror 事件的监听函数。发送的数据无法序列化成字符串时，会触发这个事件。  
self.close()：关闭 Worker 线程。  
self.postMessage()：向产生这个 Worker 线程发送消息。  
self.importScripts()：加载 JS 脚本。  
2. 子线程接受主线程消息：  
    ``` javascript
        self.addEventListener('message', function (e) {   
           console.log(e.data);   
         }, false);
   ```
   或者  
   ``` javascript
        self.onmessage=function(event){
            console.log(event.data)
        }
   ```
3. 子线程发送消息给主线程：
     ``` javascript
        var data;
        postMessage(data)
   ```
## 错误处理
主线程可以监听 Worker 是否发生错误。如果发生错误，Worker 会触发主线程的error事件。
``` javascript
worker.onerror(function (event) {
  console.log([
    'ERROR: Line ', e.lineno, ' in ', e.filename, ': ', e.message
  ].join(''));
});

// 或者
worker.addEventListener('error', function (event) {
  // ...
});
```
Worker 内部也可以监听error事件。
## 关闭worker
使用完毕，为了节省系统资源，必须关闭 Worker。
``` javascipt 
// 主线程
worker.terminate();
// Worker 线程
self.close()
```
## 通信问题
+ 子线程与主线程通信的通信内容，可以是文本，也可以是对象。需要注意的是，这种通信是**拷贝关系**，即是传值而不是传址。
+ 但是，拷贝方式发送二进制数据，会造成性能问题。比如，主线程向 Worker 发送一个 500MB 文件，默认情况下浏览器会生成一个原文件的拷贝。为了解决这个问题，JavaScript 允许主线程把二进制数据直接转移给子线程，但是一旦转移，主线程就无法再使用这些二进制数据了，这是为了防止出现多个线程同时修改数据的麻烦局面。这种转移数据的方法，叫做Transferable Objects。这使得主线程可以快速把数据交给 Worker，对于影像处理、声音处理、3D 运算等就非常方便了，不会产生性能负担。
如果要直接转移数据的控制权，就要使用下面的写法。
``` javascript
// Transferable Objects 格式
worker.postMessage(arrayBuffer, [arrayBuffer]);
// 例子
var ab = new ArrayBuffer(1);
worker.postMessage(ab, [ab]);
```
## 注意点
+ worker的脚本文件必须和主线程的脚本文件同源。  
+ worker无法访问主线程所在网页的 DOM 对象，也无法使用document、window、parent这些对象。但是，Worker 线程可以navigator对象和location对象。
+ Worker 线程不能执行alert()方法和confirm()方法，但可以使用 XMLHttpRequest 对象发出 AJAX 请求。
+ Worker 线程无法读取本地文件，即不能打开本机的文件系统（file://），它所加载的脚本，必须来自网络。
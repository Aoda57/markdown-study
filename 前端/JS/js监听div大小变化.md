# JS监听div大小/其他变化

[参考文章](https://libin1991.github.io/2019/01/01/JS%E7%9B%91%E5%90%ACdiv%E5%85%83%E7%B4%A0%E7%9A%84resize/)   

之前只了解到window.addEventListener('resize',callback);这样才能获取到关于resize的变化,但是这个resize是针对window窗口的变化,
不能得到某个元素的resize.
## MutationObserver
> 监听dom某个元素所有的变化,比如attributes获取下面的子元素,但是在监听dom变化的过程中,
> 会记录每一个DOM的变化（为一个MutationRecord对象）,将dom所有的变化记录下来,等待dom变化结束之后,再返回监听
> 到的变化队列

### 使用方法
``` javascript
    // 基于浏览器获取对应的MutationObserver的实现
    const MutationObserve = window.MutationObserver || window.WebkitMutaionObserver || window.MozMutationObserver;
    // 自定义回函数,实现当监听到元素变化,实现的内容
    const callback = (records)=>{
        for(let record of records){
            console.log(record)
        }
    }
    // 获取实例
    const observer = new MutationObserver(callback);
    // 获取元素
    const element = document.getElementById('container');
    // 配置选项
    const config = {
        attributes:true, // 是否监听attributes属性变化
        attributeFilter:['style'] // 数组,过滤attributes
        attributeOldValue:true, //获取未变化前的属性值
        childList:true, //是否监听指定元素的所有子元素.不监听指定元素
        characterData:true, // 监听元素的data变化
        characterDataOldValue:true, // 获取未变化前的data值
        subtree:true, // 是否按配置监听指定元素和所有子元素,必须配合attributes || childList || characterData之一使用
    }
    // 注册某个元素的监听
    observer.observe(element,config);
```

## ResizeObserber
> 专门监听指定元素的大小变化,用法同MutationObserver
``` javascript 
    // 新建实例
    const resizeObserver = new ResizeObserver((enties) => {
      // 编写回调函数
      for (const entiy of enties) {
        console.log("ResizeObserver earthContainer change width-height",entiy.contentRect.width,entiy.contentRect.height)
      }
    })
    // 注册监听
    resizeObserver.observe(container)
```

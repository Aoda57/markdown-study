# less 学习

## 介绍
> Less （Leaner Style Sheets 的缩写） 是一门向后兼容的 CSS 扩展语言,他是一个CSS预处理器，可以为网站启用可自定义，可管理和可重用的样式表。 LESS是一种动态样式表语言，扩展了CSS的功能。 LESS也是跨浏览器友好。   
> 
> CSS预处理器是一种脚本语言，可扩展CSS并将其编译为常规CSS语法，以便可以通过Web浏览器读取。 它提供诸如变量，函数， mixins 和操作等功能，可以构建动态CSS
## 使用
> npm install -g less   
> lessc styles.less styles.css  
//
> <link rel="stylesheet/less" type="text/css" href="styles.less" />   
> <script src="//cdnjs.cloudflare.com/ajax/libs/less.js/3.11.1/less.min.js" ></script>

## 基本规则

### 变量（Variables）
> 定义一个变量控制常用值   
+ 定义一个CSS规则值
``` less
@width: 10px;
@height: @width + 10px;

#header {
  width: @width;
  height: @height;
}
```
+ 代替CSS内的选择器名称、属性名、URL、@import语句
``` less
// Variables
@my-selector: banner;

// Usage
.@{my-selector} {
  font-weight: bold;
  line-height: 40px;
  margin: 0 auto;   
}

//预处理后
.banner {
  font-weight: bold;
  line-height: 40px;
  margin: 0 auto;
}
  ```
  + 变量也可以定义变量
``` less
@primary:  green;
@secondary: blue;

.section {
  @color: primary;

  .element {
    color: @@color;
  }
}
//预处理后
.section .element {
  color: green;
}
```
+ 属性作为变量
``` less
.widget {
  color: #efefef;
  background-color: $color; //使用$
}
//预处理后
.widget {
  color: #efefef;
  background-color: #efefef;
}
```

### 父类选择器 &
> 选择父类，用来添加伪元素或者修改类名，&代表所有父选择器（而不仅仅是最接近的祖先）
``` less
//选择父类
a {
  color: blue;
  &:hover {
    color: green;
  }
}
// 结果是：
a {
  color: blue;
}

a:hover {
  color: green;
}

// 修改类名
.button {
  &-ok {
    background-image: url("ok.png");
  }
  &-cancel {
    background-image: url("cancel.png");
  }

  &-custom {
    background-image: url("custom.png");
  }
}
// 输出：
.button-ok {
  background-image: url("ok.png");
}
.button-cancel {
  background-image: url("cancel.png");
}
.button-custom {
  background-image: url("custom.png");
}
```

### 扩展 extrend（）
> 伪类，将括号内的选择器与放置位置上的选择器合并，扩展要么附加到选择器，要么放置在规则集中
> 
> 当在扩展参数中最后指定all关键字时，它告诉Less将该选择器作为另一个选择器的一部分进行匹配。将复制选择器，然后仅将选择器的匹配部分替换为扩展名，从而创建一个新的选择器。---选择器名称的替换

>复制检测  
tips：
  + 默认情况下扩展查找选择器之间的完全匹配，必须具有相同的形式才能匹配，意义相同没有用
  + 匹配时，属性选择器中的引用类型无关紧要
  + 扩展必须放置最后一个
  + 扩展是不能够与变量匹配选择
  + 声明:extend内的内容只在 @media 一个媒体类型声明内的选择器匹配，如只在screen

``` less

nav ul {
  &:extend(.inline);
  background: blue;
}
.inline {
  color: red;
}
// 产出

nav ul {
  background: blue;
}
.inline,
nav ul {
  color: red;
}
// 选择器名称替换 all
.replacement:extend(.test all) {}
```




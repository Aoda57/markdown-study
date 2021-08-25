# grid 布局

## 介绍

> 是一种二维布局，将页面划分成不同的网格，通过行和列的方式确定具体的元素的位置

01. 容器 container 

> 采用网格布局的区域叫做容器

02.  项目 item

> 容器内部采用网格定位的子元素叫做 项目

03. 行与列

> 容器内水平的区域叫做行（row），垂直的区域叫做列（column）

04. 单元格 

> 行和列交叉的部分叫做单元格

05. 网格线

> 划分网格的线---网格线（grid-line），水平网格线划分出行，垂直网格线划分为列

## 属性

01. display :grid

> 指定容器采用网格布局，默认指定容器为块级元素，使用inline-grid ，指定容器内项目为行内元素

02. grid-template-columns、 grid-template-rows属性

> 用于划分行和列，grid-template-columns定义列宽、grid-template-rows定义行高

```css
.container {
    display: grid;
    grid-template-columns: 100px 100px 150px;
    grid-template-rows: 30px 40px 50px;
}
```

03. auto-fill关键字

> 自动填充，表示固定宽或高的项目在此水平（行或者列方向上）自动放置，直到容纳满为止

```css
.container {
    display: grid;
    grid-template-columns: repeat(auto-fill, 100px);
    grid-template-rows: repeat(auto-fill, 20px);
}
```

04. fr 关键字
   > 用于表示项目之间的比列关系，1fr 2fr

05. minmax() 函数

> 用于产生一个长度范围，表示长度在此范围内，如minmax（10px, 1fr）

06. auto关键字

> 浏览器自行决定长度

07. 网线格名称
   >grid-template-columns属性和grid-template-rows属性里面，还可以使用方括号，指定每一根网格线的名字，方便以后的引用

```css
.container {
    display: grid;
    grid-template-columns: [c1] 100px [c2] 100px [c3] auto [c4];
    grid-template-rows: [r1] 100px [r2] 100px [r3] auto [r4];
}
```

> 网格布局允许同一根线有多个名字，比如[fifth-line row-5]

08. row-gap、column-gap、gap

> 设置行或者列的间隔

09. grid-template-areas 

> 网格布局允许指定区域（area），一个区域由一个个或多个单元格组成，此属性用于定义区域

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 100px);
    grid-template-rows: repeat(3, 100px);
    grid-template-areas: "header header header"
        "main main sidebar"
        "footer footer footer";
}
```

> 相同区域用同一名字命名，区域若不需要利用，使用 .  命名

 

> 区域的命名会影响到网格线。每个区域的起始网格线，会自动命名为区域名-start，终止网格线自动命名为区域名-end

 10. grid-auto-flow 属性  

> 设置容器内项目的排列顺序，column为按列，row为按行，  
> row dense 表示先行后列，并尽可能填满区域，不出现空格，同理column 

11. justify-items align-items  place-items
    >  justify-items 设置单元格内容的水平位置，取值为start、end、center、stretch

    > align-items 设置单元格的垂直位置，具体值同上

    > place-items是前面两个属性的合并写法，如果省略第二个值，浏览器就会假定第二个值等于第一个值

12. justify-content align-content place-content
    >  justify-content 设置单元格整个内容区域在容器的水平位置，取值为start、end、center、space-around、space-evenly、space-between |、stretch

    > align-content 设置单元格整个内容区域在容器的垂直位置，具体值同上
    
    > place-content是前面两个属性的合并写法

> space-around - 每个项目两侧的间隔相等。所以，项目之间的间隔比项目与容器边框的间隔大一倍。

> space-between - 项目与项目的间隔相等，项目与容器边框之间没有间隔。
> space-evenly - 项目与项目的间隔相等，项目与容器边框之间也是同样长度的间隔。

01.  grid-auto-columns grid-auto-rows
 > 设置浏览器自动生成多余网格的属性，写法同grid-template-columns，若不设定，浏览器自动根据内容给定列宽和行高

项目属性

14.  grid-column-start、grid-column-end、grid-row-start、grid-row-end

> 指定项目的位置，通过指定项目的四个边框与哪根网格线对齐

  + grid-column-start属性：左边框所在的垂直网格线
  + grid-column-end属性：右边框所在的垂直网格线
  + grid-row-start属性：上边框所在的水平网格线
  + grid-row-end属性：下边框所在的水平网格线
  
  >如果存在重叠，可以使用z-index ，表示顺序
   >这四个属性的值还可以使用span关键字，表示"跨越"，即左右边框（上下边框）之间跨越多少个网格。span 2 表示跨越2个网格

```css
  .item-1 {
      grid-column-start: 2;
      grid-column-end: 4;
  }

  /*  指定项目1的左边框与2号网格线对齐，有边框是第四根垂直网格线，数字表示第几根网格线，也可以指定为网格线的名字*/
```

15. grid-column grid-row

> grid-column 是grid-column-start、grid-column-end的简写，同理grid-row
> 如 grid-column：1 / 3 等同

> grid-column-start：1
> grid-column-end：3

16. grid-area

> 指定项目位于哪块区域，需先设置grid-template-areas
>  
> grid-area属性还可用作grid-row-start、grid-column-start、grid-row-end、grid-column-end的合并简写形式，直接指定项目的位置。 如grid-area：1 / 1 / 3 / 3 

17. justify-self、align-self、place-self
    

> justify-self属性设置单元格内容的水平位置（左中右），跟justify-items属性的用法完全一致，但只作用于单个项目。

> align-self属性设置单元格内容的垂直位置（上中下），跟align-items属性的用法完全一致，也是只作用于单个项目。

tips：
01.  设置grid布局后，项目的float，display：inline-block、display：table-cell，vertical-align column-*都会失效

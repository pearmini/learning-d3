# D3、网页开发入门

这个仓库是用于存放“山东大学2020年可视化课程”第一次的实验课的部分教学内容的笔记和代码。

笔记内容从网页开发最基础的 HTML 讲起，涉及 SVG 的介绍，然后到 CSS 以及 JS，最后介绍 D3 的基本使用。

代码部分是一个响应式的网页，可以在电脑、平板和移动端访问。主要用 D3 对 nCov 的确诊数进行了简单的可视化，可视化的方法是条形图。这里是在线 [demo](https://pearmini.github.io/d3-barchart-demo/)。
  
## HTML

HTML 是网页的结构层，用来描述网页的结构。

HTML文档是超文本标记语言( Hyper Text Markup Language )的简称。它不是一门编程语言，是一种标记语言，用来描述网页。一般来说 HMTL 文档就是网页。

HTML 文件由一系列的标记标签和存文本组成。不同的标签有不同的性质和功能，这些标签组合在一起就是我们的页面。

下面是一个 HTML 文件基本结构。

```html
<html>
    <head>
        <!-- 一些不可见，用来描述文档信息的元素 -->
    </head>
    <body>
        <!-- 一些可见，组成页面的元素 -->
    </body>
</html>
```

### 常见的元素

```html
<!-- tab 上的标题 -->
<title>hello d3</title>

<!-- 指定使用字符集合 -->
<meta charset="utf-8">

<!-- 适配移动端 -->
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

- 块状元素：div、section、article、aside、header、footer：div 的语意不是很丰富。
- 段落、标题、图片等：p、h1、h2、img、a
- 行内元素：span、em、strong
- 列表元素：ul、ol、li、dl、dt、dd
- 表单元素：form、input、textarea、button、select
  
### DOM 节点

浏览器把 HTML 解析为一棵 DOM Tree，每一个节点就是一个 DOM 节点。

### SVG

SVG，指可缩放矢量图形（Scalable Vector Graphics），是用于描述二维矢量图形的一种图形格式。除了 IE8 之前的版本外，绝大部分浏览器都支持 SVG。

在浏览器中可以通过下面的方式使用 SVG。

```html
<svg viewBox="0 0 400 400">
    <rect 
      width="100" 
      height="200" 
      fill="red" 
      transform="translate(50, 50) rotate45)"
    />
</svg>
```

点击这里 [HTML](https://developer.mozilla.org/zh-CN/docs/Web/HTML)、[SVG](https://developer.mozilla.org/zh-CN/docs/Web/SVG) 学习更多。

## CSS

CSS(Cascading Style Sheets)，层叠样式表，是网页的表现层，用来指定网页的样式。

CSS 是由一个个选择器和对应的样式声明构成，基本语法如下。

```css
selector {
    declaration1; 
    declaration2; 
    ... 
    declarationN;
}
```

下面介绍三种最常见的选择器。

```css
/* 元素选择器 */
element {}

/* 类选择器 */
.class {}

/* id 选择器 */
#id {}
```

在 HTML 里面使用 CSS 的主要方式有三种。

（1）外部样式表

```html
<head>
    <link rel="stylesheet" type="text/css" href="index.css">
</head>
```

```css
/* index.css */
p {
   color:sienna;
   margin-left:20px;
}
```

（2）内部样式表

```html
<style>
    p {
       color:sienna;
       margin-left:20px;
    }
<style>
```

（3）内联样式

```html
<p style="color:sienna;margin-left:20px">这是一个段落。</p>
```

点击[这里](https://developer.mozilla.org/zh-CN/docs/Web/CSS)学习更多。

## JavaScript

JavaScript 是网页的行为层。

JavaScript 是一种运行在浏览器中的解释型的编程语言。

为什么起名叫 JavaScript？原因是当时 Java 语言非常红火，所以网景公司希望借 Java 的名气来推广，但事实上 JavaScript 除了语法上有点像 Java，其他部分基本上没啥关系。

### 声明变量

这里只介绍两种，也是最常用的声明变量的方法。

`let` 用于声明一个变量，`const` 用于声明一个只读的常量。一旦声明，常量的值就不能改变。

```js
let a = 1;
const b = 1;

a++; // 1
b++; // TypeError: Assignment to constant variable.
```

这特别说明一下：`const` 对于复合类型的变量，变量名不指向数据，而是指向数据所在的地址。const命令只是保证变量名指向的地址不变，并不保证该地址的数据不变，所以将一个对象声明为常量必须非常小心。

```js
const c = [];
c.append(1) // [1]
```

### 基本数据类型

（1）Number

```js
const a = 1;
const b = 0.5;
```

（2）String

```js
/* 基本使用 */
const a = 'hello world';
const b = "hello world";

/* 模版字符串 */
const name = "Jim", age = 12;
const hello = `My name is ${name}, and my age is ${age}`; // My name is Jim, and my age is 12.
```

（3）Boolean

```js
true
false
```

（4）Array

```js
const a = [1, "string", false, [2]];

a.push(4) // [1, "string", false, [2], 4];
a.length // 5
```

（5）Object

```js
const student = {
    name:"Jim",
    age:20,
    hobbies:["basketball", "badminton"],
    hello: function() {
        console.log("hello")
    }
}

student.sex = "男";
student.age = 21;
student.hello();
```

（6）null && undefined

```js
let a; // undefined
let b = null; // null
```

### 运算符

和 c 语言几乎一样，下面主要介绍一下比较运算符。

``` js
a === b // good
a == b // bad，不推荐使用

a !== b
```

### 定义函数

```js
function add(x, y){
    return x + y;
}

const add = function(x, y){
    return x + y;
}

const add = (x, y) => x + y;
```

### 判断和循环

```js
const a = [1, 2, 3];

for(let i = 0; i < a.length; i++){
    a[i] = a[i] * 2;
} // [2, 4, 6]

for(let item of a){
    item = item * 2;
} // [2, 4, 6]

a.forEach(function(item, index){
    item = item * 2;
}) // [2, 4, 6]

const b = a.map((item, index) => item * 2);
// a: [1, 2, 3]
// b: [2, 4, 6]
```

### 操作 DOM

我们可以通过 JavaScript 来对 DOM 进行操作。

（1）获得浏览器元素

```js
const element = document.querySelectorAll("selector");
```

（2）获得属性

```js
element.getAttribute("key");
```

（3）设置属性

```js
element.getAttribute("key", "value");
```

### 使用方式

这里介绍两种在 HTML 中使用脚本的方式。

（1）外部脚本

```html
<script src="app.js"></script>
```

```js
// app.js
console.log("hello world)
```

（2）内部脚本

```html
<script>
    console.log("hello world");
</script>
```

点击[这里](https://www.liaoxuefeng.com/wiki/1022910821149312)学习更多。

## D3

D3.js 是一个 JavaScript 库，用于基于数据操作文档。D3 可帮助您使用 HTML、SVG 和 CSS 使数据栩栩如生。D3 对 Web 标准的强调为您提供了现代浏览器的全部功能，而无需将自己与专有框架捆绑在一起，将强大的可视化组件和数据驱动的 DOM 操作方法相结合。

### 为什么学习

[D3](https://d3js.org/) 是一个比较底层的工具，只有知道了原理，才能更加随性所欲的可视化。

### 介绍

在我看来，我们在通过网页实现数据可视化的时候，就是在数据和 DOM 间建立映射关系（绑定），并且将数据的特征通过 DOM 对应属性（颜色、大小）来进行展示。

D3 在整个流程中都给我提供了工具。下面是安装的方式：

```html
<script src="https://d3js.org/d3.v5.min.js"></script>
```

在学习的过程中，希望同学多读[API](https://github.com/d3/d3/blob/master/API.md)和查看[案例](https://observablehq.com/@d3/gallery)。

### 读取和预处理数据

在开发过程中，学要在本地开启服务器才能正常读取数据。下面演示通过 python3 开启一个简单的服务器。

```bash
python3 -m http.server 8000
```

这里只演示读取 CSV 格式的数据。

```csv
name,age
A,10
B,20
C,30
```

```js
d3.csv("1.csv", d3.autoType).then(data => {
    console.log(data)
})
/*
[
    {name: "A", age: 10},
    {name: "B", age: 20},
    {name: "C", age: 30},
]
 * /
```

### 获得 DOM

这里要提到一个 selections 的概念，也就是返回的 DOM 元素。

```js
const rectlist = d3.selectAll("rect") //获得所有的 p 元素
const rect = d3.select("rect") // 获得第一个 p 元素

rect.style("cursor", "pointer");
rect.attr("height", 10);
```

### 数据和 DOM 绑定

当我们有了数据和 DOM 之后，就可以对它们进行绑定了。

```js
const data = [ /*... */ ];
const selections = d3.selectAll("selector");
```

我们通过 data 方法对数据进行绑定，并且将绑定好数据的 selections 分为3个部分。

```js
const upate = selections
            .data(data)
            .attr(/***/);

const enter = update
            .enter()
            .append("rect");

const exit = update
            .exit()
            .remove();
```

### 将数据的特征映射为 DOM 的属性

到了现在就需要使用到比例尺了，D3 给我们提供了丰富的比例尺，这里只介绍其中两个。

比例尺本质上一个是一个函数。

（1）首先是线性比例尺

```js
const scale = d3.scaleLinear()
    .domin([0, 10])
    .range([0, 100])

scale(0) // 0
scale(10) // 100
scale(5) // 50
```

（2）然后是序数比例尺。

```js
const scale = d3.scaleBand()
    .domin(["A", "B", "C", "D"])
    .range([0, 60])

scale("A") // 0
scale("B")  // 20
scale("C") // 40
scale("D") // 60
```

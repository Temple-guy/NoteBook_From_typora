## CSS普通流（文档流）

> W3C规范中没有`document flow`这个概念，只有[normal-flow](http://www.w3.org/TR/CSS2/visuren.html#normal-flow), 文档流的叫法主要还是多数中文译者的翻译方式问题。

### 什么是文档流

> [!NOte]
>
> 文档流是 HTML 元素在网页上的排列方式。
>
> HTML 元素分为块级元素和行内元素。块级元素在浏览器中会占满容器的宽度，后面的块级元素会在新的一行进行排列，例如 div 和 p 元素都是块级元素。
>
> 行内元素的宽度是根据内容宽度来决定的，后面如果有剩余空间，会被其它文本或者行内元素占据。
>
> 这种浏览器默认的排列方式，称为正常文档流（Normal Flow）。

### 脱离正常文档流

> [!Note]
>
> 修改文档流主要通过 display 属性、multi-column 布局、float 布局和 position 定位来实现。
>
> 它们其中有的会使元素脱离正常的文档流，可以理解为把这个元素放到了新的图层里，之前它占据的空间会被后面的元素补上。

通过 display 属性，我们可以把块级元素改为行内元素，把行内元素改为块级元素，或者行内、块级兼具的元素：

```css
display: inline;
display: block;
display: inline-block;
```

还可以设置全新的布局方式：flexbox 和 grid，子元素的布局会根据它们的设置而改变：

```css
display: flexbox;
display: grid;
```

老一代的 table 布局也是类似的：

```css
display: table;
display: table-row;
display: table-cell;
```

这些设置都不会让元素脱离正常的文档流。

CSS multi-column layout 可以进行多列布局，它也不会让元素脱离正常的文档流。

```css
column-count: 3;
```

Float 布局可以把元素移动到左侧或右侧，会使元素脱离正常文档流：

```css
float: left;
float: right;
```

对于 Postion 属性，它是针对单个元素设置定位，进行位置微调。默认为 static，即遵守正常文档流或布局设置：

```css
postion: static;
```

relatvie 可以让元素根据最近的，设置了 position 为非 static 值的父级容器，进行偏移，但不会脱离文档流：

```css
postion: relative;
top: 20px;
left: 12px;
```

接下来几个定位值，会脱离正常文档流。

- absolute
- fixed
- sticky

absolute 绝对定位，与 relative 类似，可以根据最近的，设置了 position 为非 static 值的父级容器，进行偏移，但是元素会脱离文档流：

```css
position: absolute;
top: 20px;
left: 12px;
```

fixed 固定定位，可以基于浏览器可视区域进行偏移和定位，并且永久保持在那个位置：

```css
position: fixed;
right: 0;
bottom: 0;
```

sticky 粘滞定位，它会在浏览器滚动到设置的偏移位置后，脱离文档流，并保持在这个位置：

```css
position: sticky;
top: 20px;
```

## Image Sprites[精灵图](https://blog.csdn.net/weixin_42897762/article/details/105138754)

An image sprite is a collection of images put into a single image.
图像精灵是放入单个图像中的图像集合。

A web page with many images can take a long time to load and generates multiple server requests.
包含许多图像的网页可能需要很长时间才能加载并生成多个服务器请求。

Using image sprites will reduce the number of server requests and save bandwidth.

例：**循环精灵图**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      li {
        float: left;
        background: url(mySprite.png);
        width: 50px;
        height: 50px;
        margin-left: 20px;
        list-style: none;
      }
    </style>
  </head>
  <body>
    <div>
      <ul>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
      </ul>
    </div>
    <script>
      //教程  https://blog.csdn.net/weixin_42897762/article/details/105138754
      // 1. 获取元素，所有的小li
      var lis = document.querySelectorAll("li");
      for (var i = 0; i < lis.length; i++) {
        // 让索引号乘以50就是每个小li的背景y坐标  index就是当前的y坐标
        var index = i * 50;
        // 注意，拼接字符串后得到的是，例如：0 - 50px
        lis[i].style.backgroundPosition = "0 -" + index + "px"; //字符串拼接了而已
      }
    </script>
  </body>
</html>

```

![image-20240707150112736](imgFiles\image-20240707150112736.png)原精灵图

最终变成

![image-20240707150129764](imgFiles\image-20240707150129764.png)

## Block and Inline Elements

### Block-level Elements

A block-level element always starts on a new line, and the browsers automatically add some space (a margin) before and after the element.

A block-level element always takes up the full width available (stretches out to the left and right as far as it can).

Two commonly used block elements are: `<p>` and `<div>`.

Here are the block-level elements in HTML:

`<div>`	`<p>`	`<form>`	`<footer>`	`<h1>-<h6>`

`<header>`	`<hr>`	`<li>`	`<ol>`	`<ul>`...

### Inline Elements

An inline element does not start on a new line.

An inline element only takes up as much width as necessary.

Here are the inline elements in HTML:

`<br>`	`<button>`	`<img>`	`<input>`	`<label>`...

## [position](https://developer.mozilla.org/zh-CN/docs/Web/CSS/position)

HTML elements are positioned static by default.

### position: relative

An element with `position: relative;` is positioned relative to its normal position.

### position: fixed

An element with `position: fixed;` is positioned relative to the viewport, which means it always stays in the same place even if the page is scrolled. The top, right, bottom, and left properties are used to position the element.
具有 `position: fixed;` 的元素相对于视口定位，这意味着即使滚动页面，它也始终保持在同一位置。top、right、bottom 和 left 属性用于定位元素。

### position: absolute

An element with `position: absolute;` is positioned relative to the nearest positioned ancestor (instead of positioned relative to the viewport, like fixed).
具有 `position: absolute;` 的元素相对于最近定位的祖先进行定位（而不是相对于视口进行定位，如固定）。

> [!WARNING]
>
> 1. An element with absolute positioning is always **relative to the first parent** that has a relative position;(⭐搭配relative使用)
> 2. when you use absolute positioning you place the absolutely positioned element in relation to a parent container and the parent container is the positioning context

> 例 ：输入框 
>
> 输入框和按钮都是绝对位置(position: absolute;)，相对于他们的父元素div(position: relative;)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      div {
        width: 30%;
        height: 30px;
        background-color: aquamarine;
        margin: auto;
        margin-top: 100px;
        position: relative;
      }
      input {
        position: absolute;
        right: 30px;
        top: 3px;
      }
      button {
        width: 25px;
        position: absolute;
        right: 2px;
        top: 3px;
      }
    </style>
  </head>
  <body>
    <div>
      <input type="password" />
      <button>click</button>
    </div>
    <script></script>
  </body>
</html>
```

## [center](https://blog.hubspot.com/website/center-div-css)

自动水平居中

```html
margin: auto;
width: 50%;
```

## [top / bottom / left / right](https://css-tricks.com/almanac/properties/t/top-right-bottom-left/)

The element will will generally move away from a given side when its value is positive, and towards it when the value is negative. In the example below, a positive length for `top` moves the element down (away from the top) and a negative length for `top` will move the element up (towards the top):
当元素的值为正时，元素通常会远离给定的一侧，而当值为负时，元素将向给定的一侧移动。在下面的示例中，`top` 的正长度将元素向下移动（远离顶部），`top` 的负长度将元素向上移动（朝向顶部）：

![image-20240707154250267](imgFiles\image-20240707154250267.png)

## 伪类和伪元素

`CSS` 引入伪类和伪元素概念是为了格式化文档树以外的信息，也就是说，伪类和伪元素的作用主要是用来修饰不在文档树中的部分，两者的区别如下

- 伪类用于当已有元素处于的某个状态时，为其添加对应的样式，这个状态是根据用户行为而动态变化的

  - 比如说，当用户悬停在指定的元素时，我们可以通过 `:hover` 来描述这个元素的状态

- 伪元素用于创建一些不在文档树中的元素，并为其添加样式

  - 比如说，我们可以通过 `:before` 来在一个元素前增加一些文本，并为这些文本添加样式
  - 虽然用户可以看到这些文本，但是这些文本实际上不在文档树中

  简单的总结就是

  - 伪类的操作对象是文档树中已有的元素
  - 而伪元素则创建了一个文档数外的元素

![img](imgFiles\04-01.png)

## pseudo-selector伪选择器

### [：nth-child](https://css-tricks.com/how-nth-child-works/)

![image-20240708111907742](imgFiles\image-20240708111907742.png)

```css
li:nth-child(5) {
    color: green;   
}
```

> [!Note]
>
> 注意不是从0开始，是从1开始的

```css
ul li:nth-child(3n+3) {  
  color: #ccc;
}
```

```txt
(3 x 0) + 3 = 3 = 3rd Element
(3 x 1) + 3 = 6 = 6th Element
(3 x 2) + 3 = 9 = 9th Element
etc.
```

您可以使用它来选择带有 `-n+3` 的“前 n 个元素”：

```html
-0 + 3 = 3 = 3rd Element
-1 + 3 = 2 = 2nd Element
-2 + 3 = 1 = 1st Element
-3 + 3 = 0 = no match
etc.
```

![image-20240708111847084](imgFiles\image-20240708111847084.png)

![image-20240708111756305](imgFiles\image-20240708111756305.png)

#### Select Only Odd or Even

![image-20240708112042563](imgFiles\image-20240708112042563.png)

#### Select the Second to Last Element

![image-20240708112117473](imgFiles\image-20240708112117473.png)

## [Template Literals](https://css-tricks.com/template-literals/)模版字符串

要创建模板文本，我们使用反引号 （```） 字符，而不是单引号 （`'`） 或双引号 （`"）。这将产生一个新字符串，我们可以以任何我们想要的方式使用它。 

```javascript
let newString = `A string`;
```

Template Literals 的伟大之处在于，我们现在可以创建多行字符串！过去，如果我们希望字符串位于多行上，则必须使用 `\n` 或换行符。

使用模板文字字符串，我们可以在编写新行时继续将新行添加到字符串中。

```html
var myMultiString= `This will be
on two lines!`;
```

### ${expression}

let name = `Ryan`; console.log(`Hi my name is ${name}`);

The `${}` syntax allows us to put an expression in it and it will produce the value, which in our case above is just a variable that holds a string! (可以字符串语句中添加变量).

We can evaluate any sort of expressions that we would like.

```html
let price = 19.99;
let tax = 1.13;

let total = `The total prices is ${price * tax}`;
```

We can also use this with a more complex object.

```html
let person = {
    firstName: `Ryan`,
    lastName: `Christiani`,
    sayName() {
        return `Hi my name is ${this.firstName} ${this.lastName}`;
    }
};
```

## transition

[工具网址](https://www.transition.style/#out:square:center)

## [css选择器](https://coderperson.com/2020/06/27/web-css%E5%B8%B8%E8%A7%81%E9%80%89%E6%8B%A9%E5%99%A8/#%E5%B1%9E%E6%80%A7%E9%80%89%E6%8B%A9%E5%99%A8)

属性选择器前的标签名可省略

## attribute

### opacity 不透明度

```css
/* 完全不透明 */
opacity: 1;
opacity: 1;

/* 半透明 */
opacity: 0.6;

/* 完全透明 */
opacity: 0;
opacity: 0;

opacity: inherit;

```

## 丝滑滚动

```css
//页面滚动条丝滑滚动
html {

 scroll-behavior: smooth;

}
```


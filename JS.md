## 第一章：走进JS
### 1.1认识Javascript
JavaScript主要由三部分组成
1. 核心（ECMAScript）
1. 文档对象模型（DOM）
1. 浏览器对象模型（BOM）

核心（ECMAScript）

核心规定了这门语言的基本组成部分。

有了基本组成部分，JavaScript就可以完成基本的逻辑以及数据处理。

文档对象模型（DOM）

DOM的功能：获取所有html标签，并给标签添
加或者删除样式，并可以给标签添加事件（如：点击、拖动等）；

这些功能是基于下面几种接口的：
* DOM遍历和范围： 可以找到页面中所有的标签 
* DOM事件： 给某个图片添加拖动事件，使图片可以随意拖动；
* DOM样式：可以更改页面中所有元素的样式，例如更改某一段文字的颜色。


浏览器对象模型（BOM）

BOM只会处理跟浏览器相关的东西，比如：

* 弹出新窗口功能
* 移动、缩放、关闭浏览器窗口的功能
* 给用户提供显示器分辨率的功能
* 提供浏览器信息。
### 1.2 在HTML中使用JavaScript
与CSS的书写位置非常相似，分为HTML内部和外部。
#### Javascript标签写在HTML内部
1. 使用script标签嵌入JavaScript
```
// script标签嵌入JavaScript代码
<script>
    // JavaScript代码
    let name = "Bob";
    function(){
        console.log("我的名字叫："+name);
    }
</script>

```
2. 注意script标签在HTML文件中的位置

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
  </head>
  <body>
    <!-- 正常的html标签一定要写在script标签的前面 -->
    <div></div>
    <!-- 在body标签的内部并在末尾 -->
    <script></script>
  </body>
</html>

```

>script 标签在HTML文件中的位置很随意，可以说写在哪里都无所谓，但在学习JavaScript的DOM的时候，如果不注意script标签的位置，会出现意想不到的报错
#### Javascript标签写在HTML外部
和CSS一样，在JavaScript中也推崇代码分离。通过标签去引入xxx.js文件。

引入标签如下：

` <script src='index.js'></script>`
>书写位置和写在HTML内部时一样

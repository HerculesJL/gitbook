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


### 1.3 JavaScript入门
#### 注释大致同c语言
块注释：
```
//*
*
*
*//
```
#### 字符串
单引号与双引号都可

#### 模板字符串

核心：反引号（``）与占位符${expression}。反引号的作用：将字符串和变量抱起来，占位符作用：在字符串中插入变量。
>占位符语法：${变量名}

变量名也可以是表达式
占位符例子之表达式：

```
let number1 = 20;
let number2 = 10;
console.log(`两个数的和是：${number1 + number2} 
两个数的差是：${number1 - number2} 。`);

```

占位符例子2：

```
let firstName = "胡";
let lastName = "雪岩";

let say = `大家好，我姓${firstName}，名${lastName}`;

console.log(say);

```

多行字符串拼接且有换行时，在模板字符串中直接换行就行

```
let str = `春眠不觉晓
处处闻啼鸟
夜来风雨声
花落知多少`;

console.log(str);

```
#### 模板字符串中使用三元表达式

```
let str = `这里是${false ? "浙江" : "江苏"}`;

console.log(str); // 江苏

```

使用场景一：根据屏幕的宽度来动态的更改样式。
```
// 定义屏幕的宽度，当然这个宽度是根据window的api去获取的
let screen = 760;

// 判断屏幕是大屏还是小屏，这里我们认为大于760px的就是大屏
function isLargeScreen() {
  return screen > 800;
}

// 定义元素的排列方式，大屏row排列，小屏column排列
// 具体什么排列方式，是根据屏幕大小决定的
let item = {
  isCollapsed: screen > 800
};

// 这里我们就要根据上面的信息来动态的获取类名（多个）
const classes = `header ${
  isLargeScreen() ? "" : `icon-${item.isCollapsed ? "column" : "row"}`
}`;

console.log(classes);
```

使用场景二：在JS代码中组装HTML代码。

```
let htmlCode = `
    <img src='' />
    ${
      true
        ? `<img src='https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=1906469856,4113625838&fm=26&gp=0.jpg' />`
        : `<img src='' />`
    }
`;
console.log(htmlCode);
// <img src='' />
//    <img src='https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=1906469856,4113625838&fm=26&gp=0.jpg' />


```

注意html代码作为条件成功后要输出的内容，要用反引号括起来。
#### 转义符 \
在双引号之间使用双引号"我是\\"天才\\""

在模板字符串中使用反引号

## 第五章：循环
### 5.1 for循环
#### 普通for循环
格式同c语言，只不过定义i时使用let
#### for..in和for..of
for..in循环遍历的结果是数组的下标，for..of循环遍历的结果是元素的值。
1. for..in
```
let peppaFamily = ["佩奇", "乔治", "猪妈妈", "猪爸爸"];

for (let i in peppaFamily) {
  console.log(peppaFamily[i]);
}
// 输出:
// 佩奇
// 乔治
// 猪妈妈
// 猪爸爸
```

2. for..of
```
let peppaFamily = ["佩奇", "乔治", "猪妈妈", "猪爸爸"];

for (let item of peppaFamily) {
  console.log(item);
}
// 输出:
// 佩奇
// 乔治
// 猪妈妈
// 猪爸爸

```
### 5.2 while循环
## 第六章：函数
### 6.2自定义函数
#### 两种声明方法：function命令和函数表达式。
1. function命令格式：
![image-3.png](./image-3.png)

1. 函数表达式
![image-4.png](./image-4.png)
![image-5.png](./image-5.png)


#### 函数声明的提升
![image-6.png](./image-6.png)


#### 两种声明方式的区别
![image-7.png](./image-7.png)

#### 函数的重复声明
![image-8.png](./image-8.png)

#### 立即执行函数

![image-9.png](./image-9.png)

### 6.5内置函数--计时器
定时执行代码函数 setTimeout()和setInterval()

#### 1.延时执行setTimeout()

用于指定某个函数或者某段代码在多少毫秒之后执行。他返回一个整数，表示定时器的编号，可以用于取消该定时器。

基础语法：
```
let timerId= setTimeout(fun/code,delay)

```

其中fun是函数，delay是推迟执行的毫秒数。

#### 2.验证码的倒计时
递归调用书写计时器

```
// 首先定义计时总秒数，单位 s
let i = 60;

// 定义变量用来储存定时器的编号
let timerId;

// 写一个函数，这个函数即每次要执行的代码，能够完成上述的 1、2、3
function count() {
  console.log(i);
  i--;
  if (i > 0) {
    timerId = setTimeout(count, 1000);
  } else {
    // 清除计时器
    clearTimeout(timerId);
  }
}

// 首次调用该函数，开始第一次计时
count();

```

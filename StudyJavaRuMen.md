## 第一章、Java是如何运行的
### 一、创建JAVA类文件
### 二、JAVA包管理器
#### 1.关于包(package)
` 包的路径格式为 com.youkeda.mode.Invoice`
1. 包路径采用'.'分割
1. 包路径不是绝对的文件路径，是相对Java工程目录的路径
#### 2.包名的规范
#### 3.自定义包
1. 自定义包就是创建文件夹
1. 如果在某个包下创建Java文件，那么Java类的内容就需要多一个声明包路径的语法

    比如 com.youkeda.app.Hello.java这样的Java类
    创建好的代码如下：
    ```
    package com.youkeda.app;
    public class Hello{
    }
    ```
    *注意：一个文件只有一个package语句；*
    *如果域名是lol.com 那么包路径应该是com.lol*
## 第二章、创建对象
### 2.2对象变量
#### (1).变量名
变量名的首字母要小写

>字符串类型变量初始化需要加双引号

如：`String userName = new String("joe");`

>数字类型变量初始化不需要加

如：`Integer num1 = new Integer(value:100);`
#### (2).关键词
关键词不能用作变量名

### 2.3方法调用
#### (1).实例化已有的对象
直接进行new Tex() 然后再加上.var就行。（Tex指代要实例化的对象）

>例如：**(实现环境为IDE)**

`new TextField().var`

#### (2)对于TODO项目
继承自Verticallayout的Todo类可以直接使用

`add(x) x为要添加的组件名，是一个对象`

来添加组件

垂直布局中添加的组件是竖着排布的;若改成继承Horizantallayout则会变成水平布局

TextField类对象的setlable("string")方法可以在添加的输入框前添加文本；
setPlaceholder("string")设置输入框内的默认文本(不是具体内容，只是类似于提示文本的样式)
setValue("string")会覆盖placeholder的内容 其内容为实在的默认文本

## 第三章、方法进阶
### 3.1、Button按钮
>直接new Button就行,Button对象拥有许多方法
```
1. setText()设置button的文本
2. 当然也可以直接用构造函数 ：new Button("string")
 
```
### 3.2 Lambda表达式
1.事件：例如按按钮给出响应的能力
2.可以使用Lambda来支持事件行为；
3.需要在定义button对象后(假设命名为loginButton)调用
> **注意大括号的存在**
```
loginButton.addClickListener(click->{
sout("login");
}
)
```
>如上定义后，点击button会输出login；

4.tips：调用userNameField.getValue()可以获得在输入框usernameField输入的字符串。
### 3.3逻辑语句
简单的if语句判断罢了
### 3.4自定义方法

方法的语法格式：
```
public 返回类型 方法名称(方法参数){
    代码块
}
```

### 3.5注解
1.初步判断:位于类前的 形如`@Route("/") `的语句

2.注解可以作用于类之上，方法之上，对象之上。

3.有@说明应该是注解

4.route注解用于完成多个页面的配置。`@Route("/login.html")` 加在类之前后，就可以指定页面的路径为login.html;

## 第四章、面向对象
### 4.1概要
使用到的知识点：

* 对象的封装

>把用户数据封装成Java能识别的User对象

* 日期对象

>比如用户的注册事件，一般会存储为计算机的日期类型，这样既能减少内存的存储空间，又能做日期运算

* 封装对象的数据操作
>比如User对象的数据读写

* 集合和循环
>存储多个注册用户

* 常量
>完成对象的存储
### 4.2封装User对象
**封装事务的类对象，会存放在xxx.model这个子包里(也就是model文件夹下)**

抽象成类对象后，下一步就是封装事物的属性，比如用户信息就包含了两个属性：
* 用户名
* 密码



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

### 4.3 LocalDateTime

1. LocalDate类对象的now()方法会返回日期
1. LocalTime类对象的now()方法会返回当前时间
1. LocalDateTime类对象的now()方法会返回日期以及时间 `默认格式为：2021-10-27T22:10:27`
1. 借助于DateTimeFormatter类对象可以设置输出日期的格式。

```
LocalDateTime now = LocalDateTime.now();

DateTimeFormatter dtf = DateTimeFormatter.ofPattern("yyyy/MM/dd HH:mm:ss");

String now = dtf.format(now);

System.out.println(now);
```

1. 将字符串转为日期类型的对象 `调用parse方法`

```
String str1 = "2021/10/27 22:45:00"

LocaoDateTime.parse(str1,dtf);//dtf用于指定格式，注意dtf的格式需要和string中的相匹配。
```

### 4.4 接口的介绍
引入:如何支持多个用户的注册？

解决：借助Java的集合存储。
1. 接口是一个抽象类型，是抽象方法的集合，通常用interface来声明。
1. 接口可以视为一堆方法的集合，一个接口可有多种实现。
1. Java中的集合有专门的接口定义。Collection这个接口就可以表明支持存储多个元素。Collection接口又有三种子类型，List、Set和Queue(他们都继承于Collection)，在下面是一些抽象类，最后是具体实现类，常用的有ArrayList、LinkedLisy、HashSet、HashMap等。
1. 集合框架是一个用来代表和操作集合的同意框架。所有的集合框架都包含如下内容：

```
* 接口：是代表集合的抽象数据类型，如Collection、List、Set、Map等。之所以定义多个接口，是为了以不同的方式操作集合对象

* 实现(类)：是集合接口的具体实现。从本质上讲，它们是可重复使用的数据结构，例如：ArrayList、HashSet、HashMap。

* 算法：是实现集合接口的对象里的方法执行的一些有用的计算。例如：搜索和排序。这些算法被称为多态，那是因为相同的方法可以在相似的接口上有着不同的实现。
```

除了集合，框架也定义了Map接口和类。
下面是关于集合类的架构：

![集合类的架构](https://qgt-style.oss-cn-hangzhou.aliyuncs.com/img/course/j200/java-coll.png)

> 一般来说，最常用的是List接口于他的实现类ArrayList

### 4.5 ArrayList
ArrayList类是一个可以动态修改的数组。没有固定大小的限制，可以添加或删除元素。
![](https://qgt-style.oss-cn-hangzhou.aliyuncs.com/img/course/j200/ArrayList.png)
>在Java中接口不能被直接实例化，若像创建一个接口类型的变量，需要new来实现*类*。

例如：
```
List<String> strings = new ArrayList();

// 创建一个用户集合，用于存储多个用户信息
List<User> users = new ArrayList<>();
```

下面介绍ArrayList类带的几个方法：

```
* add() //添加操作
* get(i) //获得第i+1个对象
* remove(i) //删除第i+1个对象
* clear()//删除整个集合
```

>for循环格式`for(Score score1:scores) `scores是Score类型的集合（如ArrayList类型的）；


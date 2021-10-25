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
#### 1.变量名
变量名的首字母要小写

>字符串类型变量初始化需要加双引号

如：`String userName = new String("joe");`

>数字类型变量初始化不需要加

如：`Integer num1 = new Integer(value:100);`
#### 2.关键词
关键词不能用作变量名
### 方法调用

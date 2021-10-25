# Java是如何运行的
## 创建JAVA类文件
## JAVA包管理器
### 关于包(package)
` 包的路径格式为 com.youkeda.mode.Invoice`
1. 包路径采用'.'分割
1. 包路径不是绝对的文件路径，是相对Java工程目录的路径
### 包名的规范
### 自定义包
1. 自定义包就是创建文件夹
1. 如果在某个包下创建Java文件，那么Java类的内容就需要多一个声明包路径的语法

    比如 com.youkeda.app.Hello.java这样的Java类
    创建好的代码如下：
    ```
    package com.youkeda.app;
    public class Hello{
    }
    ```
    *注意：一个文件只有一个package语句*

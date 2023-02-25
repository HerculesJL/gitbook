## 第一章Spring 入门
### 1.1 Spring的核心

依赖注入（DI）是Spring最核心的技术点，Spring所有的技术方案都是基于DI来发展的

### 1.2 Maven入门（上）

Apache Maven是一个项目管理和构建自动化工具。（我将他与jdk放在了同意目录下，他也需要环境配置）

下图是一个Maven的系统框架
![](https://style.youkeda.com/img/ham/course/j4/mvn.svg)

Maven采用惯例优于配置的原则。要求没有定制之前，所有项目都要拥有相同结构：

目录                                                 目的 

${basedir}                                      存放 pom.xml 和所有的子目 录 

${basedir}/pom.xml                     Maven 的项目配置文件 

${basedir}/src/main/java            项目的 java 源代码 

${basedir}/src/main/resources  项目的资源，比如说 property 文件

 ${basedir}/src/test/java              项目的测试类，比如说 JUnit 代码 

${basedir}/src/test/resources     测试使用的资源

这里的 ${basedir}代表的是 Java 工程的根路径，在我们这里就 是工程的根目录啦。一个 Maven 项目在默认情况下会产生 JAR (Java 的一种压缩格式)文件，另外 ，编译后 的 classes 会放在 ${basedir}/target/classes 下面， JAR 文件会放在 ${basedir}/target 下面。



Maven命令（** 需要在根目录下执行** ）

1. mvn clean complie
编译命令，会自动扫描src/main/java下的代码并完成编译工作，执行完，会在根目录下生成target/classes目录（存放所有的class）

2. mvn clean package

编译并打包命令，是complie和package的集合，会先执行complie命令，然后在执行jar打包命令，这个的结果会把所有的java文件和资源打包成一个jar，jar是java的一个压缩格式，方便我们灵活的运用多个代码。

3. mvn clean install

执行安装命令，这个命令是compile、package和install的集合，会依次执行compile、jar和install命令。install命令安装jar到本地的Maven仓库目录里。该目录是：${user_home}/.m2

4. mvn compile exec:java -Dexec.mainClass= ${main}

意思是在compile执行完后，执行运行java的命令，执行的Java类是由-Dexec.mainClass= ${main}参数决定的。
若要执行com.youkeda.Test类，则完整的命令是：

mvn compile exec:java -Dexec.mainClass=com.youkeda.Test

**Maven学习的重点是掌握它的配置文件pom.xml**

### 1.3 Maven入门（中）

Maven的核心概念

![](https://style.youkeda.com/img/ham/course/j4/Maven%E6%A0%B8%E5%BF%83%E6%A6%82%E5%BF%B5.png?x-oss-process=image/resize,w_800/watermark,image_d2F0ZXJtYXNrLnBuZz94LW9zcy1wcm9jZXNzPWltYWdlL3Jlc2l6ZSx3XzEwMA==,t_60,g_se,x_10,y_10)

这五个概念都会运用与Maven的配置文件中，其配置文件时一个XML格式文件，文件名一定是pom.xml。

#### 1、POM（Project Object Model）

一个Java项目所有的配置都放置在POM文件中。

![](https://style.youkeda.com/img/ham/course/j4/pomxml.svg)

1.1 Maven坐标

坐标是一种位置信息，Maven坐标决定了Maven工程部署后存在Maven仓库的文件位置，所以坐标信息是必须要指定的。

> Maven工程执行完后把整个工程大包成packaging指定的文件格式，如果pom.xml中没有声明packaging这个标签，那么默认情况下会打包成jar格式

1.2 Maven属性配置

Maven的属性配置是用来做参数设置的。常见配置如下

```
<properties>
    <java.version>1.8</java.version>
    <maven.compiler.source>${java.version}</maven.compiler.source>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.target>${java.version}</maven.compiler.target>
</properties>
```

* maven.complier.source 

  > 该参数用于指定Maven编译时候源代码的JDK版本。${java.version}是一个动态值，此处就是1.8

#### 1.4 Maven入门（下）

**1、依赖管理 dependencies**

用于指定当前工程依赖其他代码库。Maven会自动管理jar依赖

> 一旦在pom.xml中声明了dependency信息，会先去本地用户目录下的.m2文件夹中查找对应的文件，如果没有找到那么会触发从中央仓库下载行为，下载完会保存在本地的.m2文件夹内。

```
<dependencies>
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>fastjson</artifactId>
        <version>1.2.62</version>
    </dependency>
</dependencies>
```

可以看到dependency标签的内容其实就是Maven坐标，所以只要有坐标我们就可以建立依赖。

> 一般将别人写的代码称为三方库，自己的成为二方库

##### 1.1中央仓库

Maven将所有的jar存放在中央仓库中：https://search.maven.org/   ；

阿里云：https://maven.aliyun.com/mvn/search

##### 1.2间接依赖

间接依赖是mvn成功的核心要素，简单来说，如果一个remote工程依赖了okhttp库，而当前工程locale依赖了remote工程，那么这时候locale工程也会自动依赖okhttp。

**2、插件体系plugins**

```
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.1</version>
        </plugin>
    </plugins>
</build>
```

可以发现Maven的插件其实也是存放在中央仓库的坐标，也就是一切都是jar。



#### 1.5 Hello Spring

Spring5 的Maven坐标如下

```
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-context</artifactId>
  <version>5.2.6.RELEASE</version>
</dependency>
```

Spring 强调的是面向接口编程，所以大多数情况下Spring代码都会有接口和实现类。


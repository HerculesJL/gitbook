## Spring 入门
### 1.2 Maven入门
Apache Maven是一个项目管理和构建自动化工具。

下图是一个Maven的系统框架
![](https://style.youkeda.com/img/ham/course/j4/mvn.svg)

Maven命令（** 需要在根目录下执行** ）

1. mvn clean complie
编译命令，会自动扫描src/main/java下的代码并完成编译工作，执行完，会在根目录下生成target/classes目录（存放所有的class）

2. mvn clean package

编译并打包命令，是complie和package的集合，会先执行complie命令，然后在执行jar打包命令，这个的结果会把所有的java文件和资源打包成一个jar，jar是java的一个压缩格式，方便我们灵活的运用多个代码。

3. mvn clean install

执行安装命令，这个命令是compile、package和install的集合，会依次执行compile、jar和install命令。install命令安装jar到本地的Maven仓库目录里。

4. mvn compile exec:java -Dexec.mainClass= ${main}

意思是在compile执行完后，执行运行java的命令，执行的Java类是由-Dexec.mainClass= ${main}参数决定的。
若要执行com.youkeda.Test类，则完整的命令是：

mvn compile exec:java -Dexec.mainClass=com.youkeda.Test

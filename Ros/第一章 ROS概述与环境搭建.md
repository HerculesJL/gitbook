## 1.3 ROS快速体验

### 1.3.1 HelloWorld实现简介

ROS中的程序即便使用不同的编程语言，实现流程也大致类似，以当前HelloWorld程序为例，实现流程大致如下：

1. 先创建一个工作空间；
2. 再创建一个功能包；
3. 编辑源文件；
4. 编辑配置文件；
5. 编译并执行。

#### 1.创建工作空间并初始化

```
mkdir -p 自定义空间名称/src
cd 自定义空间名称
catkin_make
```

上述命令，首先会创建一个工作空间以及一个 src 子目录，然后再进入工作空间调用 catkin_make命令编译。

#### 2.进入 src 创建 ros 包并添加依赖

```
cd src
catkin_create_pkg 自定义ROS包名 roscpp rospy std_msgs
```

上述命令，会在工作空间下生成一个功能包，该功能包依赖于 roscpp、rospy 与 std_msgs，其中roscpp是使用C++实现的库，而rospy则是使用python实现的库，std_msgs是标准消息库，创建ROS功能包时，一般都会依赖这三个库实现。

**注意:** 在ROS中，虽然实现同一功能时，C++和Python可以互换，但是具体选择哪种语言，需要视需求而定，因为两种语言相较而言:C++运行效率高但是编码效率低，而Python则反之，基于二者互补的特点，ROS设计者分别设计了roscpp与rospy库，前者旨在成为ROS的高性能库，而后者则一般用于对性能无要求的场景，旨在提高开发效率。



### 1.3.2 HelloWorld(C++版)

本节内容基于1.3.1，假设你已经创建了ROS的工作空间，并且创建了ROS的功能包，那么就可以进入核心步骤了，使用C++编写程序实现：

#### 1.进入 ros 包的 src 目录编辑源文件

```
cd 自定义的包
```

C++源码实现(文件名自定义)

```cpp
#include "ros/ros.h"

int main(int argc, char *argv[])
{
    //执行 ros 节点初始化
    ros::init(argc,argv,"hello");
    //创建 ros 节点句柄(非必须)
    ros::NodeHandle n;
    //控制台输出 hello world
    ROS_INFO("hello world!");

    return 0;
}
```

#### 2.编辑 ros 包下的 Cmakelist.txt文件

```cmake
add_executable(步骤3的源文件名
  src/步骤3的源文件名.cpp
)
target_link_libraries(步骤3的源文件名
  ${catkin_LIBRARIES}
)
```

#### 3.进入工作空间目录并编译

```
cd 自定义空间名称
catkin_make
```

生成 build devel ....

#### 4.执行

**先启动命令行1：**

```
roscore
```

**再启动命令行2：**

```
cd 工作空间
source ./devel/setup.bash
rosrun 包名 C++节点
```

命令行输出: HelloWorld!

**PS:**`source ~/工作空间/devel/setup.bash`可以添加进`.bashrc`文件，使用上更方便

添加方式1: 直接使用 gedit 或 vi 编辑 .bashrc 文件，最后添加该内容

添加方式2:`echo "source ~/工作空间/devel/setup.bash" >> ~/.bashrc`

### 1.3.3 HelloWorld(Python版)

本节内容基于1.3.1，假设你已经创建了ROS的工作空间，并且创建了ROS的功能包，那么就可以进入核心步骤了，使用Python编写程序实现：

#### 1.进入 ros 包添加 scripts 目录并编辑 python 文件

```
cd ros包
mkdir scripts
Copy
```

新建 python 文件: (文件名自定义)

```py
#! /usr/bin/env python

"""
    Python 版 HelloWorld

"""
import rospy

if __name__ == "__main__":
    rospy.init_node("Hello")
    rospy.loginfo("Hello World!!!!")
```

#### 2.为 python 文件添加可执行权限（python独有的）

```
chmod +x 自定义文件名.py
```

#### 3.编辑 ros 包下的 CamkeList.txt 文件

```
catkin_install_python(PROGRAMS scripts/自定义文件名.py
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
Copy
```

#### 4.进入工作空间目录并编译

```
cd 自定义空间名称
catkin_make
```

#### 5.进入工作空间目录并执行

**先启动命令行1：**

```
roscore
```

**再启动命令行2：**

```
cd 工作空间
source ./devel/setup.bash
rosrun 包名 自定义文件名.py
```

输出结果:`Hello World!!!!`

### 1.4 ROS集成开发环境搭建

#### 1.4.2 安装VScode

#### 4.vscode 使用_基本配置

##### 4.1 创建 ROS 工作空间

```
mkdir -p xxx_ws/src(必须得有 src)
cd xxx_ws
catkin_make
Copy
```

##### 4.2 启动 vscode

进入 xxx_ws 启动 vscode

```
cd xxx_ws
code .
Copy
```

##### 4.3 vscode 中编译 ros

由于在vscode中需要频繁编译，所以配置一下编译相关的命令。

快捷键 ctrl + shift + B 调用编译，选择:`catkin_make:build`

可以点击配置设置为默认，修改.vscode/tasks.json 文件

```json
{
// 有关 tasks.json 格式的文档，请参见
    // https://go.microsoft.com/fwlink/?LinkId=733558
    "version": "2.0.0",
    "tasks": [
        {
            "label": "catkin_make:debug", //代表提示的描述性信息
            "type": "shell",  //可以选择shell或者process,如果是shell代码是在shell里面运行一个命令，如果是process代表作为一个进程来运行
            "command": "catkin_make",//这个是我们需要运行的命令
            "args": [],//如果需要在命令后面加一些后缀，可以写在这里，比如-DCATKIN_WHITELIST_PACKAGES=“pac1;pac2”
            "group": {"kind":"build","isDefault":true},  //关键点
            //“isDefault":true 意味着直接ctrl+shift+b就会编译
            "presentation": {
                "reveal": "always"//可选always或者silence，代表是否输出信息
            },
            "problemMatcher": "$msCompile"
        }
    ]
}

```

> //“isDefault":true 意味着直接ctrl+shift+b就会编译

##### 4.4 创建 ROS 功能包

选定 src 右击 ---> create catkin package

**设置包名 添加依赖**

在上方键入就行

##### 4.5 C++ 实现

**在功能包的 src 下新建 cpp 文件**

```cpp
/*
    控制台输出 HelloVSCode !!!

*/
#include "ros/ros.h"

int main(int argc, char *argv[])
{
    setlocale(LC_ALL,"");
    //执行节点初始化
    ros::init(argc,argv,"HelloVSCode");

    //输出日志
    ROS_INFO("Hello VSCode!!!哈哈哈哈哈哈哈哈哈哈");
    return 0;
}
Copy
```

**PS1: 如果没有代码提示**

修改 .vscode/c_cpp_properties.json

设置 "cppStandard": "c++17"

**PS2: main 函数的参数不可以被 const 修饰**

**PS3: 当ROS__INFO 终端输出有中文时，会出现乱码**

[INFO](http://www.autolabor.com.cn/book/ROSTutorials/chapter1/14-ros-ji-cheng-kai-fa-huan-jing-da-jian/142-an-zhuang-vscode.html#): ????????????????????????

解决办法：在函数开头加入下面代码的任意一句

```cpp
setlocale(LC_CTYPE, "zh_CN.utf8");
setlocale(LC_ALL, "");
```

##### 4.6 python 实现

在 功能包 下新建 scripts 文件夹，添加 python 文件，**并添加可执行权限**

```py
#! /usr/bin/env python
"""
    Python 版本的 HelloVScode，执行在控制台输出 HelloVScode
    实现:
    1.导包
    2.初始化 ROS 节点
    3.日志输出 HelloWorld


"""

import rospy # 1.导包

if __name__ == "__main__":

    rospy.init_node("Hello_Vscode_p")  # 2.初始化 ROS 节点
    rospy.loginfo("Hello VScode, 我是 Python ....")  #3.日志输出 HelloWorld

```

##### 4.7 配置 CMakeLists.txt

C++ 配置:

```
add_executable(节点名称
  src/C++源文件名.cpp
)
target_link_libraries(节点名称
  ${catkin_LIBRARIES}
)
Copy
```

Python 配置:

```
catkin_install_python(PROGRAMS scripts/自定义文件名.py
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
Copy
```

##### 4.8 编译执行

编译: ctrl + shift + B

执行: 和之前一致，只是可以在 VScode 中添加终端，首先执行:`source ./devel/setup.bash`



如果不编写配置文件直接执行 python 文件，会抛出异常。

1.第一行解释器声明，可以使用绝对路径定位到 python3 的安装路径 #! /usr/bin/python3，但是不建议

2.建议使用 #!/usr/bin/env python 但是会抛出异常 : /usr/bin/env: “python”: 没有那个文件或目录

3.解决1: #!/usr/bin/env python3 直接使用 python3 但存在问题: 不兼容之前的 ROS 相关 python 实现

4.解决2: 创建一个链接符号到 python 命令:`sudo ln -s /usr/bin/python3 /usr/bin/python`

### 1.4.3 launch文件演示

#### 1.需求

> 一个程序中可能需要启动多个节点，比如:ROS 内置的小乌龟案例，如果要控制乌龟运动，要启动多个窗口，分别启动 roscore、乌龟界面节点、键盘控制节点。如果每次都调用 rosrun 逐一启动，显然效率低下，如何优化?

官方给出的优化策略是使用 launch 文件，可以一次性启动多个 ROS 节点。

#### 2.实现

1. 选定功能包右击 ---> 添加 launch 文件夹

2. 选定 launch 文件夹右击 ---> 添加 launch 文件

3. 编辑 launch 文件内容

   ```
   <launch>
       <node pkg="helloworld" type="demo_hello" name="hello" output="screen" />
       <node pkg="turtlesim" type="turtlesim_node" name="t1"/>
       <node pkg="turtlesim" type="turtle_teleop_key" name="key1" />
   </launch>
   Copy
   ```

   - node ---> 包含的某个节点
   - pkg -----> 功能包
   - type ----> 被运行的节点文件
   - name --> 为节点命名
   - output-> 设置日志的输出目标

4. 运行 launch 文件

   `roslaunch 包名 launch文件名`

5. 运行结果: 一次性启动了多个节点


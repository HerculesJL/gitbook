## 第一章 Vue配置
### 1.1 Vue配置
1. 需要使用到node.js包含的npm（包管理工具）
1. 需要安装Vue CLC(脚手架)，简单来说就是Vue工程的升级版，会使得项目更容易实现。安装方法：
    ```
    npm install -g @vue/cli
    ```
    如果安装缓慢 可以切换镜像：
    ```
    sudo npm install -g cnpm --registry=https://registry.npm.taobao.org
    ```
    >sudo是mac需要添加的
    切换镜像后
    ```
    // 注意这里要用的是cnpm
    cnpm install -g @vue/cli
    ```
1. Vue工程的创建
    ```
    // vue 创建 工程名
    vue create vue_first
    ```
    >创建后在c：//users下
    自定义配置选项勾选Babel、Router选项即可
1. 创建完成在http://localhost:8080/ 
即可查看
### 1.2 Vue工程目录介绍
![image.png](https://qgt-document.oss-cn-beijing.aliyuncs.com/P3-5-Vue/1/img/src-explain.png?x-oss-process=image/resize,w_800/watermark,image_d2F0ZXJtYXNrLnBuZz94LW9zcy1wcm9jZXNzPWltYWdlL3Jlc2l6ZSx3XzEwMA==,t_60,g_se,x_10,y_10)

①：assets：存放项目中需要用到的资源文件，css、js、images 等。
②：componets: 存放 vue 开发中一些公共组件：例如项目初始的
header.vue、footer.vue 就是公共组件。 ③：router：vue 路由的配置
文件。 ④：views：存放页面文件 ⑤：app.vue：根组件 ⑥：
main.js：项目的入口文件，定义了 vue 实例，并引入根组件
app.vue，将其挂载到 index.html 中 id 为‘app’的节点上。




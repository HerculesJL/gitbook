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
![image.png](.Image/vue-src-explain.png)



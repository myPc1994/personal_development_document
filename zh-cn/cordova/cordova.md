# cordova的使用
# [官网](http://cordova.axuer.com/docs/zh-cn/latest/guide/overview/index.html)
# [w3cschool教程](https://www.w3cschool.cn/cordova/)
# 使用教程

## 安装Android或者IOS的环境

## 安装Cordova CLI
    Cordova命令行工具作为npm包分发。
    安装cordova命令行工具，通过下面这些步骤:
    1、下载和安装Node.js。安装完成后你可以在命令行中使用node 和 npm 。
    2、(可选)下载和安装git client, 如果你没有。安装成功后，你可以在命令行中使用git。 这个命令行使用下载git仓库中的资源。
    3、安装cordova 模块使用Nodejs的npm工具。cordova模块会被npm工具自动下载。
不要使用cnpm安装，建议全部使用npm全程
```shell
    $ npm install -g cordova
```
## 查看版本
```shell
cordova -v
```

## 创建App
跳转到你维护源代码的目录中，并创建你的cordova项目：
```shell
$ cordova create hello com.example.hello HelloWorld

cordova create  子项目名    package包名   应用名
```
这将会为你的cordova应用创造必须的目录。默认情况下，cordova create命令生成基于web的应用程序的骨骼，项目的主页是 www/index.html 文件。

## 支持平台查看
```shell
执行cordova platforms ls，检查你的电脑支持的平台
```

## 添加平台
给你的App添加目标平台。我们将会添加'ios'和'android'平台，并确保他们保存在了config.xml中:
```shell
$ cordova platform add ios --save
$ cordova platform add android --save
```
## 检查你当前平台设置状况:
```shell
$ cordova platform ls
```
## 安装构建先决条件
要构建和运行App，你需要安装每个你需要平台的SDK。另外，当你使用浏览器开发你可以添加 browser平台，它不需要任何平台SDK。

## 检测你是否满足构建平台的要求:
```shell
$ cordova requirements
Requirements check results for android:
Java JDK: installed .
Android SDK: installed
Android target: installed android-19,android-21,android-22,android-23,Google Inc.:Google APIs:19,Google Inc.:Google APIs (x86 System Image):19,Google Inc.:Google APIs:23
Gradle: installed

Requirements check results for ios:
Apple OS X: not installed
Cordova tooling for iOS requires Apple OS X
Error: Some of requirements check failed
```

## 构建App

默认情况下, cordova create生产基于web应用程序的骨架，项目开始页面位于www/index.html 文件。任何初始化任务应该在www/js/index.js文件中的deviceready事件的事件处理函数中。

运行下面命令为所有添加的平台构建:

```shell
$ cordova build
```
你可以在每次构建中选择限制平台范围 - 这个例子中是'android':
$ cordova build android

## 测试App

>移动平台的SDK通常会绑定模拟器，它是一个可执行的设备镜像，这样你就可以在主屏幕启动你的App，看看它在多个平台是如何交互的。 在命令行运行下面的命令，会重新构建App并可以在特定平台的模拟器上查看:

```shell
$ cordova emulate android
```
> 将你的手机插入电脑，在手机上直接测试App:

```shell
$ cordova run android
```



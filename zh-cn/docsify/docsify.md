## docsify的使用

> 无需构建快速生成文档页

> 官方文档：https://docsify.js.org/#/zh-cn/quickstart

#### 1、安装 docsify-cli 工具，可以方便创建及本地预览文档网站
```sh
  $ npm i docsify-cli -g
```
#### 2、如果想在项目的 ./docs 目录里写文档，直接通过 init 初始化项目。

```sh
  $ docsify init docs
```
#### 3.运行一个本地服务器，来预览效果，默认访问 http://localhost:3000
```sh
  $ docsify serve
```
#### 4、文档结构的介绍
> 初始化成功后，可以看到 ./docs 目录下创建的几个文件
+ index.html 入口文件
+ README.md 会做为主页内容渲染
+ .nojekyll 用于阻止 GitHub Pages 会忽略掉下划线开头的文件
+ 直接编辑 docs/README.md 就能更新网站内容
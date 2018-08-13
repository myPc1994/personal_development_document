## less的使用
> vue-cli 构建的项目默认是不支持 less 的，需要自己添加。

#### 1、安装 less 和 less-loader
```sh
  $ npm install less less-loader --save-dev
```

#### 2、安装成功后，打开build/webpack.base.conf.js
```javascript
module.exports = {
    //  此处省略无数行，已有的的其他的内容
    module: {
        rules: [
          //  此处省略无数行，已有的的其他的规则
          //添加如下规则
          {
            test: /\.less$/,
            loader: "style-loader!css-loader!less-loader",
          }
        ]
    }
}
```
#### 3、在代码中的 style 标签中 加上 lang="less" 属性即可
```less
<style scoped lang="less">

</style>
```

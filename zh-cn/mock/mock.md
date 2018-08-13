# [mock官网](http://mockjs.com/)

## 1、安装`mockjs`
```shell
npm install mockjs --save-dev
```
## 2、新建一个新的`mock.js`文件，编写mock语句
```javascript
// 引入mockjs
const Mock = require('mockjs');
import {mockFormat} from "./mockFormat";

/**
 * 指定被拦截的 Ajax 请求的响应时间，单位是毫秒。值可以是正整数，例如 400，表示 400 毫秒 后才会返回响应内容；也可以是横杠 '-' 风格的字符串，例如 '200-600'，表示响应时间介于 200 和 600 毫秒之间。默认值是'10-100'。
 */
Mock.setup({
  timeout: '500-2000'
})

// Mock.mock( url, post/get , 返回的数据)；
Mock.mock('/mock/goodsList', 'get', mockFormat.goodsList);
Mock.mock('/mock/goodsNewList', 'get', mockFormat.goodsNewList);
```
## 3、新建文件`mockFormat.js`，并编写如下
```javascript
export const mockFormat = {};
//返回某种固定格式的模拟数据,模板如下
// mockFormat.index = {
//   'infos|1-10':[
//     {
//       "姓名":'@cname',
//       "身份证":'@id',
//       "地址":'@county(true)',
//       "邮编":'@zip',
//       "邮箱":'@email',
//       "日期":'@date(yyyy年MM月dd日 HH:mm:ss)',
//       "头像":"@image",
//       "描述":'@cparagraph(1)',
//       "ip":"@ip",
//       "pick":"@pick(['第一个', '第二个', '第三个', '第四个', '第五个'])",//随机选择其中一个
//       "sss|1-100":1,//产生1-100的数据
//       'regexp1': /[a-z][A-Z][0-9]/,//利用正则表达式反向生成
//       'pic':"@dataImage('150x150', 'mock模拟的图片')"
//     }
//   ]
// };
/**
 * 商品列表
 */
mockFormat.goodsList = {
  code:200,
  'goods|10-15':[
    {
      "title":"@cparagraph(1)",
      "describe":"@cparagraph(2)",
      "sellingPrice|999-2000":1,
      "realPrice|2000-2300":1,
      "img":"@dataImage('150x150', '模拟的图片')",
      "right":"@pick(['竞价成功', '竞价成功'])"
    }
  ]
}
/**
 * 新的商品列表数据
 */
mockFormat.goodsNewList = {
  code:200,
  'goods|0-5':[
    {
      title:"新的数据",
      "describe":"@cparagraph(2)",
      "sellingPrice|999-2000":1,
      "realPrice|2000-2300":1,
      "img":"@dataImage('150x150', '模拟的图片')",
      "right":"@pick(['竞价成功', '竞价成功'])"
    }
  ]
}

```

## 4、在main.js里面引入该`mock.js`文件
```javascript
// 引入mockjs
require('./mock.js')
```


# mock语法的示例代码
```javascript
// 引入mockjs
const Mock = require('mockjs');
// 获取 mock.Random 对象
const Random = Mock.Random;

// 通过逻辑模拟一组数据
const produceNewsData = function() {
  let articles = [];
  for (let i = 0; i < 100; i++) {
    let newArticleObject = {
      title: Random.csentence(5, 30), //  Random.csentence( min, max )
      thumbnail_pic_s: Random.dataImage('300x250', 'mock的图片'), // Random.dataImage( size, text ) 生成一段随机的 Base64 图片编码
      author_name: Random.cname(), // Random.cname() 随机生成一个常见的中文姓名
      date: Random.date() + ' ' + Random.time() // Random.date()指示生成的日期字符串的格式,默认为yyyy-MM-dd；Random.time() 返回一个随机的时间字符串
    }
    articles.push(newArticleObject)
  }
  return {
    articles: articles
  }
}


//返回某种固定格式的模拟数据
const index = {
  'infos|1-10':[
    {
      "姓名":'@cname',
      "身份证":'@id',
      "地址":'@county(true)',
      "邮编":'@zip',
      "邮箱":'@email',
      "日期":'@date(yyyy年MM月dd日 HH:mm:ss)',
      "头像":"@image",
      "描述":'@cparagraph(1)',
      "ip":"@ip",
      "pick":"@pick(['第一个', '第二个', '第三个', '第四个', '第五个'])",//随机选择其中一个
      "sss|1-100":1,//产生1-100的数据
      'regexp1': /[a-z][A-Z][0-9]/,//利用正则表达式反向生成
      'pic':"@dataImage('150x150', 'mock模拟的图片')"
    }
  ]
};



// Mock.mock( url, post/get , 返回的数据)；
Mock.mock('/news/index', 'post', index);
Mock.mock('/news/yyy', 'get', produceNewsData);

```
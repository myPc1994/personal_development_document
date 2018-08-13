# 正常使用
## 1、安装vue-axios
```shell
npm install axios --save
```
## 2、在main.js中将axios绑定到VUE的原型链上即可
```javascript
Vue.prototype.$http = axios
```
## 3、在vue界面中调用
```javascript
this.$http.get(url, params)
.then(res=>{
    console.log("请求成功了",res)
})
.catch(error=>{
    console.log("请求失败",error)
})
```

>上面的方式存在问题,v和m的耦合性太高了，也不利于后期的维护

# 新的方式

## 1、安装vue-axios
```shell
npm install axios --save
```
## 2、新建三个文件，分别如下：
    https.js//网络请求的逻辑处理
    urls.js//网络请求的地址
    httpIntercept.js//网络请求的拦截器

## 3、三个文件分别如下:
`https.js`
```javascript
import {urls} from './urls'
import {Axios} from './httpIntercept'

export const https = {};
/**
 * 获取main界面的page数据
 * @param params
 * @returns {Promise}
 */
https.getPage = (url,params) => {
  return new Promise((resolve, reject) => {
    Axios.get(urls.mainPage1, params).then(res => {
      console.log("得到服务端的数据",res)
      //逻辑处理后再返回
      resolve(res.data);
    }).catch(err => {
      reject(err);
    })
  })
}
__https= https;

```

`urls.js`
```javascript
export const urls = {};
//获取main界面的page数据
urls.mainPage1='地址1';
//主页面2
urls.mainPage2='地址2';

```

`httpIntercept.js`
```javascript
import axios from "axios";
export const Axios = axios.create({
  timeout: 10000,
  responseType: "json",
  withCredentials: true, // 是否允许带cookie这些
  headers: {
    "Content-Type": "application/x-www-form-urlencoded;charset=utf-8"
  }
});

//POST传参序列化(添加请求拦截器)
Axios.interceptors.request.use(
  config => {
    return config;
  },
  error => {
    return Promise.reject(error.data.error.message);
  }
);

//返回状态判断(添加响应拦截器)
Axios.interceptors.response.use(
  res => {
    return res;
  },
  error => {
    return Promise.reject(error);
  }
);

```
## 4、在`main.js`中调用一下
```javascript
import {https} from './https/https'
```
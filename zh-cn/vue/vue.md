# VUE的知识点


### 1、路由却换动画
在`app.vue`的文件下，修改
```vue
  <template>
    <div id="app">
      <transition :name="transitionName">
        <router-view class="Router"></router-view>
      </transition>
    </div>
  </template>

  <script>
    export default {
      name: 'App',
      data() {
        return {
          transitionName: 'slide-right'  // 默认动态路由变化为slide-right
        }
      },
      watch: {
        '$route'(to, from) {
          let isBack = this.$router.isBack  //  监听路由变化时的状态为前进还是后退
          this.transitionName = isBack ? 'slide-right' : 'slide-left';
          this.$router.isBack = false
        }
      }
    }
  </script>

  <style>
    .Router {
      position: absolute;
      width: 100%;
      transition: all .8s ease;
    }

    .slide-left-enter,
    .slide-right-leave-active {
      opacity: 0;
      transform: translate3d(100%, 0, 0);
    }

    .slide-left-leave-active,
    .slide-right-enter {
      opacity: 0;
      transform: translate3d(-100%, 0, 0);
    }
  </style>
```
在路由的`index.js`文件下绑定后退处理,主要是做isBack状态值得变化
```javascript
/**
 * 绑定一个后退在路由的原型链上，以后后退都调用这个即可
 */
Router.prototype.goBack = function () {
  this.isBack = true
  window.history.go(-1)
}

```
在需要返回的地方调用
```javascript
$router.goBack()
```
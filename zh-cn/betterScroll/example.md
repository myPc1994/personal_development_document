<div style='background: #000 url("/images/honor7x.jpg");
                  width: 360px;
                  height: 730px;
                  -webkit-background-size: 100%;
                  background-size: 100%;
                  position: fixed;
                  top: 80px;
                  right: 20px;'>
  <iframe style='width: 320px;height: 645px;position: absolute;top: 30px;left: 20px;' name="mainIframe" src="../../myApp/index.html" frameborder="0" scrolling="auto" width="360px" height="500px"></iframe>
</div>




#  better-Scroll的示例
##  基础使用

### 1、滚动效果
<a href="../../myApp/index.html#/cpcBaseScroll" target="mainIframe" >效果展示</a>
```vue
<template>
  <cpcBaseScroll>
    <p v-for="item in 50">年后</p>
  </cpcBaseScroll>
</template>

<script type="text/ecmascript-6">
  import cpcBaseScroll from '../../CPCUI/scroll/baseScroll/cpcBaseScroll.vue'
  export default {
    components: {cpcBaseScroll},
    data() {
      return {}
    },
    props: {},
    methods: {},
    computed: {},
    mounted() {

    },
    destroyed() {

    }
  }
</script>

<style scoped lang="less">

</style>

```
`cpcBaseScroll`的属性
<table style="width:100%;text-align:center;">
    <tr>
        <th width="10%">参数</th>
        <th  width="60%">说明</th>
        <th  width="10%">类型</th>
        <th  width="10%">可选值</th>
        <th  width="10%">默认值</th>
    </tr>
    <tr>
        <td>height</td>
        <td>高度</td>
        <td>String</td>
        <td>-</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>probeType</td>
        <td>
        是否截流<br>
        1 滚动的时候会派发scroll事件，会截流。 <br>
        2 滚动的时候实时派发scroll事件，不会截流。 <br>
        3 除了实时派发scroll事件，在swipe的情况下仍然能实时派发scroll事件 <br>
        </td>
        <td>Number</td>
        <td>1,2,3</td>
        <td>1</td>
    </tr>
    <tr>
        <td>click</td>
        <td>点击列表是否派发click事件</td>
        <td>Boolean</td>
        <td>-</td>
        <td>true</td>
    </tr>
    <tr>
       <td>scrollX</td>
       <td>是否开启横向滚动</td>
       <td>Boolean</td>
       <td>-</td>
       <td>false</td>
    </tr>
    <tr>
       <td>scroll</td>
       <td>是否派发滚动事件</td>
       <td>Boolean</td>
       <td>-</td>
       <td>false</td>
    </tr>
    <tr>
       <td>touchEnd</td>
       <td>是否派发触摸结束事件</td>
       <td>Boolean</td>
       <td>-</td>
       <td>false</td>
     </tr>
     <tr>
       <td>beforeScrollStart</td>
       <td>是否派发列表滚动开始的事件</td>
       <td>Boolean</td>
       <td>-</td>
       <td>false</td>
    </tr>
     <tr>
       <td>scrollEnd</td>
       <td>是否派发滚动结束事件</td>
       <td>Boolean</td>
       <td>-</td>
       <td>false</td>
     </tr>
     <tr>
       <td>pullDownRefresh</td>
       <td>设置下拉刷新开启的参数</td>
       <td>[Boolean, Object]</td>
       <td>-</td>
       <td>false</td>
     </tr>
</table>

`cpcBaseScroll`的方法
<table style="width:100%;text-align:center;">
    <tr>
        <th width="10%">事件名称</th>
        <th  width="20%">说明</th>
        <th  width="60%">形参</th>
        <th  width="10%">回调参数</th>
    </tr>
     <tr>
       <td>_initScroll</td>
       <td>初始化滚动</td>
       <td>-</td>
       <td>-</td>
     </tr>
     <tr>
        <td>disable</td>
        <td>禁用 better-scroll，DOM 事件（如 touchstart、touchmove、touchend）的回调函数不再响应</td>
        <td>-</td>
        <td>-</td>
    </tr>
    <tr>
        <td>enable</td>
        <td>启用 better-scroll, 默认 开启</td>
        <td>-</td>
        <td>-</td>
    </tr>
    <tr>
        <td>refresh</td>
        <td>重新计算 better-scroll，当 DOM 结构发生变化的时候务必要调用确保滚动的效果正常</td>
        <td>-</td>
        <td>-</td>
    </tr>
    <tr>
        <td>scrollTo</td>
        <td>滚动到指定的位置</td>
        <td>
        x, y, time, easing <br>
        {Number} x 横轴坐标（单位 px）<br>
        {Number} y 纵轴坐标（单位 px）<br>
        {Number} time 滚动动画执行的时长（单位 ms）<br>
        {Object} easing 缓动函数，一般不建议修改，如果想修改，参考源码中的 ease.js 里的写法<br>
        </td>
        <td>-</td>
    </tr>

    <tr>
        <td>scrollToElement</td>
        <td>滚动到指定的目标元素。</td>
        <td>
        el, time, offsetX, offsetY, easing <br>
        {DOM | String} el 滚动到的目标元素, 如果是字符串，则内部会尝试调用 querySelector 转换成 DOM 对象。<br>
        {Number} time 滚动动画执行的时长（单位 ms）<br>
        {Number | Boolean} offsetX 相对于目标元素的横轴偏移量，如果设置为 true，则滚到目标元素的中心位置<br>
        {Number | Boolean} offsetY 相对于目标元素的纵轴偏移量，如果设置为 true，则滚到目标元素的中心位置<br>
        {Object} easing 缓动函数，一般不建议修改，如果想修改，参考源码中的 ease.js 里的写法<br>
        </td>
        <td>-</td>
    </tr>
     <tr>
            <td>finishPullDown</td>
            <td>当下拉刷新数据加载完毕后，需要调用此方法告诉 better-scroll 数据已加载</td>
            <td>-</td>
            <td>-</td>
        </tr>
    <tr>
        <td>finishPullUp</td>
        <td>当上拉加载数据加载完毕后，需要调用此方法告诉 better-scroll 数据已加载</td>
        <td>-</td>
        <td>-</td>
    </tr>
</table>


### 2、下拉刷新的类型1
<a href="../../myApp/index.html#/cpcRefreshType1" target="mainIframe" >效果展示</a>

```vue
<template>
  <cpcRefreshType1 ref="cpcRefreshType1" @loading="loading" @loadMore="loadMore">
    <button @click="$router.goBack()">后退</button>
    <cpcSingleRow2  v-for="item in lll" :datas="row2"></cpcSingleRow2>
  </cpcRefreshType1>
</template>

<script type="text/ecmascript-6">
  import cpcRefreshType1 from '../../../CPCUI/refresh/type/cpcRefreshType1.vue'
  import cpcSingleRow2 from '../../../CPCUI/cards/singleRow/type/cpcSingleRow2.vue'

  export default {
    components: {cpcRefreshType1,cpcSingleRow2},
    data() {
      let lll = new Array(20)
      return {
        lll:lll,
        row2: {
          img: "./static/images/logo.png",
          title: "标题标题标题标题标题标题标题标题",
          describe: "描述内容描述内容描述内容描述内容描述内容描述内容描述内容描述内容描述内容描述内容描述内容描述内容描述内容描述内容",
          sellingPrice: 420,
          realPrice: "原价500",
          right: "竞价成功"
        }
      }
    },
    props: {},
    methods: {
      loading(finishPullDown) {
        setTimeout(() => {
          let arr = new Array(5)
          this.lll.unshift(...arr)
          finishPullDown();
        }, 2000)
      },
      loadMore(finishpullUp,setLoadMoreALL) {
        setTimeout(() => {
          let arr = new Array(5)
          this.lll.push(...arr)
          finishpullUp();
          if (arr.length == 0) {
            setLoadMoreALL(true);
          }
        }, 2000)
      }
    },
    computed: {},
    mounted() {

    },
    destroyed() {

    }
  }
</script>

<style scoped lang="less">

</style>


```


`cpcRefreshType1`的方法
<table style="width:100%;text-align:center;">
    <tr>
        <th width="10%">事件名称</th>
        <th  width="60%">说明</th>
        <th  width="20%">形参</th>
        <th  width="10%">回调参数</th>
    </tr>
     <tr>
       <td>loading</td>
       <td>下拉刷新触发的事件</td>
       <td>-</td>
       <td>-</td>
     </tr>
     <tr>
        <td>loadMore</td>
        <td>加载更多触发的事件</td>
        <td>-</td>
        <td>-</td>
    </tr>
</table>
> 当`下拉刷新`结束后，需要调用this.$refs.cpcRefreshType1.`finishPullDown()`;方法 ，让状态恢复正常<br>
> 当`上拉加载更多`结束后，需要调用this.$refs.cpcRefreshType1.`finishpullUp()`;方法 ，让状态恢复正常<br>
> 当`上拉加载更多`没有最近数据，需要调用this.$refs.cpcRefreshType1.`setLoadMoreALL(true)`;方法 ，让下拉加载更多不在产生<br>





### 3、下拉刷新的类型2
<a href="../../myApp/index.html#/cpcRefreshType2" target="mainIframe" >效果展示</a>

```vue
<template>
  <cpcRefreshType2 ref="cpcRefreshType1" @loading="loading" @loadMore="loadMore">
    <button @click="$router.goBack()">后退</button>
    <cpcSingleRow2  v-for="item in lll" :datas="row2"></cpcSingleRow2>
  </cpcRefreshType2>
</template>

<script type="text/ecmascript-6">
  import cpcRefreshType2 from '../../../CPCUI/refresh/type/cpcRefreshType2.vue'
  import cpcSingleRow2 from '../../../CPCUI/cards/singleRow/type/cpcSingleRow2.vue'
  export default {
    components: {cpcRefreshType2,cpcSingleRow2},
    data() {
      let lll = new Array(20)
      return {
        lll,
        row2: {
          img: "./static/images/logo.png",
          title: "标题标题标题标题标题标题标题标题",
          describe: "描述内容描述内容描述内容描述内容描述内容描述内容描述内容描述内容描述内容描述内容描述内容描述内容描述内容描述内容",
          sellingPrice: 420,
          realPrice: "原价500",
          right: "竞价成功"
        }
      }
    },
    props: {},
    methods: {
      loading(finishPullDown) {
        setTimeout(() => {
          let arr = new Array(5)
          this.lll.unshift(...arr)
          finishPullDown();
        }, 2000)
      },
      loadMore(finishpullUp,setLoadMoreALL) {
        setTimeout(() => {
          let arr = new Array(5)
          this.lll.push(...arr)
          finishpullUp();
          if (arr.length == 0) {
            setLoadMoreALL(true);
          }
        }, 2000)
      }
    },
    computed: {},
    mounted() {

    },
    destroyed() {

    }
  }
</script>

<style scoped lang="less">

</style>

```

`cpcRefreshType2`的方法
<table style="width:100%;text-align:center;">
    <tr>
        <th width="10%">事件名称</th>
        <th  width="60%">说明</th>
        <th  width="20%">形参</th>
        <th  width="10%">回调参数</th>
    </tr>
     <tr>
       <td>loading</td>
       <td>下拉刷新触发的事件</td>
       <td>-</td>
       <td>-</td>
     </tr>
     <tr>
        <td>loadMore</td>
        <td>加载更多触发的事件</td>
        <td>-</td>
        <td>-</td>
    </tr>
</table>
> 当`下拉刷新`结束后，需要调用this.$refs.cpcRefreshType1.`finishPullDown()`;方法 ，让状态恢复正常<br>
> 当`上拉加载更多`结束后，需要调用this.$refs.cpcRefreshType1.`finishpullUp()`;方法 ，让状态恢复正常<br>
> 当`上拉加载更多`没有最近数据，需要调用this.$refs.cpcRefreshType1.`setLoadMoreALL(true)`;方法 ，让下拉加载更多不在产生<br>


### 4、轮播图的示例
<a href="../../myApp/index.html#/banner" target="mainIframe" >效果展示</a>
> 轮播图的第一个就是了，名称为：cpcBanner1




## 高级使用

### 1、自定义刷新的样式
<a href="../../myApp/index.html#/customRefreshScroll" target="mainIframe" >效果展示</a>

```vue
<template>
  <cpcBaseRefresh ref="refreshScroll" @loading="loading" @loadMore="loadMore">
    <div slot="statePulldown">
      <img width="50px" height="50px" src="../../assets/logo.png" alt="">
      下拉刷新
    </div>
    <div slot="stateRelease">
      <img width="50px" height="50px" src="../../assets/logo.png" alt="">
      释放刷新
    </div>
    <div slot="stateRefreshing">刷新中</div>
    <div slot="stateRefreshEnd">刷新完成</div>
    <p v-for="item in lll">{{item}}new</p>
    <loading slot="loadMoreing"></loading>
    <div slot="loadMores">加载更多</div>
    <div slot="loadMoreALL">加载全部了</div>
  </cpcBaseRefresh>
</template>

<script>
  import cpcBaseRefresh from '../../CPCUI/scroll/refresh/cpcBaseRefresh.vue'
  import loading from '../../CPCUI/animate/loading/loading.vue';

  export default {
    components: {cpcBaseRefresh,loading},
    name: 'HelloWorld',
    data() {
      return {
        msg: 'Welcome to Your Vue.js App',
        lll: [
          "你好", "你好", "你好", "你好", "你好", "你好", "你好", "你好", "你好", "你好",
          "你好", "你好", "你好", "你好", "你好", "你好", "你好", "你好", "你好", "你好",
          "你好", "你好", "你好", "你好", "你好", "你好", "你好", "你好", "你好", "你好",
          "你好", "你好", "你好", "你好", "你好", "你好", "你好", "你好", "你好", "你好",
          "你好", "你好", "你好", "你好", "你好", "你好", "你好", "你好", "你好", "你好",
          "你好", "你好", "你好", "你好", "你好", "你好", "你好", "你好", "你好", "你好",

        ],
      }
    },
    methods: {
      loading() {
        setTimeout(() => {
          let arr = new Array(5)
          this.lll.unshift(...arr)
          this.$refs.refreshScroll.finishPullDown();
        }, 2000)
      },
      loadMore() {
        setTimeout(() => {
          let arr = new Array(5)
          this.lll.push(...arr)
          this.$refs.refreshScroll.finishpullUp();
          if (arr.length == 0) {
            this.$refs.refreshScroll.loadMoreALL = true;
          }
        }, 2000)
      }
    }
  }
</script>

<style scoped>

</style>

```

`cpcBaseRefresh`的slot
<table style="width:100%;text-align:center;">
    <tr>
        <th width="10%">slot名称</th>
        <th  width="60%">说明</th>
        <th  width="30%">限制</th>
    </tr>
     <tr>
       <td>statePulldown</td>
       <td>用户处于负屏，但没有达到刷新的条件，展示的内容</td>
       <td>-</td>
     </tr>
     <tr>
        <td>stateRelease</td>
        <td>用户处于负屏，达到刷新的条件，展示的内容</td>
        <td>-</td>
    </tr>
     <tr>
        <td>stateRefreshing</td>
        <td>刷新中,展示的内容</td>
        <td>-</td>
    </tr>
     <tr>
        <td>stateRefreshEnd</td>
        <td>刷新完成,展示的内容</td>
        <td>-</td>
    </tr>
     <tr>
        <td>loadMoreing</td>
        <td>加载更多中，展示的内容</td>
        <td>cpcBaseRefresh内部状态值:`loadMoreALL`必须处于false</td>
    </tr>
     <tr>
        <td>loadMores</td>
        <td>用户滑动到底部，告知用户当前处于底部状态了的内容，再过200ms触发加载更多事件</td>
        <td>cpcBaseRefresh内部状态值:`loadMoreALL`必须处于false</td>
    </tr>
     <tr>
        <td>loadMoreALL</td>
        <td>当后台没有更多数据了，告知用户没办法在加载最新数据展示的内容</td>
        <td>cpcBaseRefresh内部状态值:`loadMoreALL`必须处于true</td>
    </tr>
</table>
`cpcBaseRefresh`的props
<table style="width:100%;text-align:center;">
    <tr>
        <th width="10%">属性名称</th>
        <th  width="60%">说明</th>
        <th  width="20%">默认值</th>
        <th  width="10%">是否必须</th>
    </tr>
    <tr>
        <td>isFreshType</td>
        <td>刷新的类型:Number<br>0 : 同时拥有下拉刷新和上拉加载更多<br>1 : 只有下拉刷新<br>2 : 只有上拉加载更多<br>其他: 都没有</td>
        <td>0</td>
        <td>否</td>
    </tr>
</table>
`cpcBaseRefresh`的方法
<table style="width:100%;text-align:center;">
    <tr>
        <th width="10%">事件名称</th>
        <th  width="60%">说明</th>
        <th  width="20%">形参</th>
        <th  width="10%">是否允许调用</th>
    </tr>
    <tr>
        <td>finishPullDown</td>
        <td>刷新完成调用</td>
        <td>-</td>
        <td>允许</td>
    </tr>
    <tr>
        <td>finishpullUp</td>
        <td>加载更多完成调用</td>
        <td>-</td>
        <td>允许</td>
    </tr>
     <tr>
       <td>setLoadMoreALL</td>
       <td>设置是否允许触发加载更多事件</td>
       <td>state:true;  Boolean状态值</td>
       <td>允许</td>
     </tr>
     <tr>
        <td>scroll</td>
        <td>触摸结束触发的事件</td>
        <td>pos:{x:0,y:0}  Object 坐标信息</td>
        <td>不允许</td>
    </tr>
    <tr>
        <td>scrollEnd</td>
        <td>滑动结束触发的事件</td>
        <td>pos:{x:0,y:0} Object 坐标信息</td>
        <td>不允许</td>
    </tr>
</table>
##
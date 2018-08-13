# better-scroll
### npm的方式使用
####  1、`better-scroll` 托管在 `npm` 上，执行如下命令安装：
``` sh
    //npm
    npm install better-scroll --save
    //淘宝镜像
    cnpm install better-scroll --save
```
####  2、接下来就可以在代码中引入了，`webpack` 等构建工具都支持从`node_modules`里引入代码：
```javascript
    //ES6语法
    import BScroll from 'better-scroll
    //ES5语法
    var BScroll = require('better-scroll')
```

### 使用script标签引入
```html
    <script src="https://unpkg.com/better-scroll@1.0.1/dist/bscroll.min.js"></script>
```

## 封装

### 1、滑动的基类 `cpcBaseScroll.vue`

```vue
<template>
  <div ref="wrapper" :style="{height:height,overflow:'hidden'}">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>
<script type="text/ecmascript-6">
  import BScroll from 'better-scroll'

  export default {
    props: {
      height: {
        type: String,
        default: "100%"
      },
      /**
       * 1 滚动的时候会派发scroll事件，会截流。
       * 2 滚动的时候实时派发scroll事件，不会截流。
       * 3 除了实时派发scroll事件，在swipe的情况下仍然能实时派发scroll事件
       */
      probeType: {
        type: Number,
        default: 1
      },
     //点击列表是否派发click事件
      click: {
        type: Boolean,
        default: true
      },
      //是否开启横向滚动
      scrollX: {
        type: Boolean,
        default: false
      },
      //是否派发滚动事件
      scroll: {
        type: Boolean,
        default: false
      },
      //是否派发触摸结束事件
      touchEnd: {
        type: Boolean,
        default: false
      },
      //是否派发列表滚动开始的事件
      beforeScrollStart: {
        type: Boolean,
        default: false
      },
      //是否派发滚动结束事件
      scrollEnd: {
        type: Boolean,
        default: false
      },
      //设置下拉刷新开启的参数
      pullDownRefresh: {
        type: [Boolean, Object],
        default: false
      }
    },
    mounted() {
      this.$nextTick(() => {
        this._initScroll()
      })
    },
    methods: {
      _initScroll() {
        if (!this.$refs.wrapper) {
          return
        }
        // better-scroll的初始化
        this.BaseScroll = new BScroll(this.$refs.wrapper, {
          probeType: this.probeType,
          click: this.click,
          scrollX: this.scrollX,
          pullDownRefresh: this.pullDownRefresh,
        })
        // 是否派发滚动事件
        if (this.scroll) {
          let me = this
          this.BaseScroll.on('scroll', (pos) => {
            me.$emit('scroll', pos)
          })
        }
        // 是否派发滚动结束事件
        if (this.scrollEnd) {
          this.BaseScroll.on('scrollEnd', (pos) => {
            this.$emit('scrollEnd', pos, this.BaseScroll.maxScrollY)
          })
        }
        //是否派发触摸结束事件
        if (this.touchEnd) {
          this.BaseScroll.on('touchEnd', (pos) => { // 下拉动作
            this.$emit('touchEnd', pos)
          })
        }
        // 是否派发列表滚动开始的事件
        if (this.beforeScrollStart) {
          this.BaseScroll.on('beforeScrollStart', (pos) => {
            this.$emit('beforeScrollStart',pos)
          })
        }
      },
      disable() {
        // 代理better-scroll的disable方法
        this.BaseScroll && this.BaseScroll.disable()
      },
      enable() {
        // 代理better-scroll的enable方法
        this.BaseScroll && this.BaseScroll.enable()
      },
      refresh() {
        // 代理better-scroll的refresh方法
        this.BaseScroll && this.BaseScroll.refresh()
      },
      scrollTo() {
        // 代理better-scroll的scrollTo方法
        this.BaseScroll && this.BaseScroll.scrollTo.apply(this.BaseScroll, arguments)
      },
      scrollToElement() {
        // 代理better-scroll的scrollToElement方法
        this.BaseScroll && this.BaseScroll.scrollToElement.apply(this.BaseScroll, arguments)
      },
      finishPullDown() {
        // 代理better-scroll的scrollToElement方法
        this.BaseScroll && this.BaseScroll.finishPullDown.apply(this.BaseScroll, arguments)
      },
      finishPullUp() {
        // 代理better-scroll的scrollToElement方法
        this.BaseScroll && this.BaseScroll.finishPullUp.apply(this.BaseScroll, arguments)
      }
    }
  }
</script>
<style scoped lang="less">
  .content {
    position: relative;
    min-height: calc(~"100% + 1px");
  }
</style>

```
### 2、下拉刷新基类`cpcBaseRefresh.vue`

```vue
<template>
  <cpcBaseScroll ref="cscroll" class="cpc-base-scroll"
                 :scrollEnd="true"
                 @scrollEnd="scrollEnd"
                 :touchEnd="true"
                 @touchEnd="touchEnd"
                 :pullDownRefresh="pullDownState?pullDownRefresh:false"
                 :scroll="true"
                 @scroll="scroll">
    <div v-if="pullDownState" class="pullDown">
      <!--下拉刷新-->
      <div v-show="!freshState0 && !freshState1 && !freshState2">
        <slot name="statePulldown"></slot>
      </div>
      <!--释放刷新-->
      <div v-show="!freshState0 && freshState1 && !freshState2">
        <slot name="stateRelease"></slot>
      </div>
      <!--刷新中-->
      <div v-show="freshState0">
        <slot name="stateRefreshing"></slot>
      </div>
      <!--刷新完成-->
      <div v-show="!freshState0 && freshState2">
        <slot name="stateRefreshEnd"></slot>
      </div>
    </div>
    <slot></slot>
    <div v-if="pullUpState" class="pullUp" >
      <!--加载更多中-->
      <div v-show="!loadMoreALL && loadMoreState">
        <slot name="loadMoreing"></slot>
      </div>
      <!--加载更多-->
      <div v-show="!loadMoreALL && !loadMoreState">
        <slot name="loadMores"></slot>
      </div>
      <!--加载全部了-->
      <div v-if="loadMoreALL">
        <slot name="loadMoreALL"></slot>
      </div>
    </div>
  </cpcBaseScroll>
</template>

<script type="text/ecmascript-6">
  import cpcBaseScroll from '../scroll/baseScroll/cpcBaseScroll.vue'

  export default {
    components: {cpcBaseScroll},
    data() {
      return {
        freshState0: false,//刷新中的状态
        freshState1: false,//是否达到刷新的节点
        freshState2: false,//刷新是否完成
        isShowPullUp: true,//是否展示加载更多
        loadMoreState: false,//加载更多
        loadMoreALL: false,//已经加载全部了
        pullDownRefresh: {
          threshold: 50,
          stop: 50
        }
      }
    },
    props: {
//      刷新的类型：0 支持下拉刷新，和下拉加载更多，1：只有上拉刷新，2：只有下拉加载更多
      isFreshType: {
        type: Number,
        default: 0
      }
    },
    methods: {
      /**
       * 是否全部加载完毕
       */
      setLoadMoreALL(flag) {
        this.loadMoreALL = flag;
      },
      /**
       * 是否启动加载更多
       */
      setIsShowPullUp(flag) {
        this.isShowPullUp = flag;
      },
      scroll(pos) {
        if (pos.y > 50) {
          this.freshState1 = true;
        } else {
          this.freshState1 = false;
        }
      },
      /**
       * 触摸结束触发的事件
       */
      touchEnd(pos) {
        if(!this.pullDownState)return;
        if (!this.freshState0 && pos.y > 50) {
          console.log("下拉刷新")
          this.freshState0 = true;
          this.$emit("loading")
        } else {
          this.$refs.cscroll.finishPullDown();
        }
      },
      /**
       * 刷新完成调用
       */
      finishPullDown() {
        console.log("下拉刷新结束")
        this.freshState0 = false;
        this.freshState2 = true;
        setTimeout(() => {
          this.$refs.cscroll.finishPullDown();
          this.$refs.cscroll.refresh()
          setTimeout(() => {
            this.freshState2 = false;
          }, 300)
        }, 1000)
      },
      /**
       * 滑动结束触发的事件
       */
      scrollEnd(pos) {

        let dis = this.$refs.cscroll.BaseScroll.maxScrollY;
        if (dis < -51) {
          this.isShowPullUp = true;
        } else {
          this.isShowPullUp = false;
        }
        if(!this.pullUpState)return;
        if ( !this.loadMoreALL && !this.loadMoreState && pos.y <= dis + 50) {
          clearTimeout(this.LoadMoreTimer);
          this.LoadMoreTimer = setTimeout(() => {
            this.$emit("loadMore")
            this.loadMoreState = true;
            console.log("下拉加载更多")
          }, 200)
        }else{
          console.log(this.isShowPullUp,dis)
        }
      },
      /**
       * 加载更多完成调用
       */
      finishpullUp() {
        console.log("下拉加载更多结束")
        this.loadMoreState = false;
        this.$refs.cscroll.finishPullUp()
        this.$nextTick(() => {
          this.$refs.cscroll.refresh()
        })

      }
    },
    computed: {
      pullDownState(){
        return this.isFreshType==0||this.isFreshType==1;
      },
      pullUpState(){
        return (this.isFreshType==0||this.isFreshType==2)  && this.isShowPullUp;
      }
    },
    mounted() {
      this.$nextTick(() => {
        let maxY = this.$refs.cscroll.BaseScroll.maxScrollY;
        if (maxY > -50) {
          this.isShowPullUp = false;
        } else {
          this.isShowPullUp = true;
        }
      })
    },
    destroyed() {

    }
  }
</script>

<style scoped lang="less">
  .cpc-base-scroll {
    height: 100%;
    .pullDown {
      width: 100%;
      text-align: center;
      height: 50px;
      line-height: 50px;
      position: absolute;
      top: -50px;
      left: 0;
      overflow: hidden;
      > div {
        height: 100%;
      }
    }

    .pullUp {
      width: 100%;
      position: relative;
      text-align: center;
      height: 50px;
      line-height: 50px;
      overflow: hidden;
      > div {
        height: 100%;
      }
    }
  }
</style>


```
### 3、提供刷新的样式-简单的文字
```vue
<template>
  <cpcBaseRefresh ref="refreshScroll" @loading="loading" @loadMore="loadMore">
    <span slot="statePulldown">下拉刷新</span>
    <span slot="stateRelease">释放刷新</span>
    <span slot="stateRefreshing">刷新中</span>
    <span slot="stateRefreshEnd">刷新完成</span>
    <slot></slot>
    <loading slot="loadMoreing"></loading>
    <span slot="loadMores">加载更多</span>
    <span slot="loadMoreALL">加载全部了</span>
  </cpcBaseRefresh>
</template>

<script>
  import cpcBaseRefresh from '../../refresh/cpcBaseRefresh.vue'
  import loading from '../../../animate/loading/loading.vue';

  export default {
    components: {cpcBaseRefresh, loading},
    data() {
      return {}
    },
    methods: {
      setLoadMoreALL() {
        this.$refs.refreshScroll && this.$refs.refreshScroll.setLoadMoreALL.apply(this.$refs.refreshScroll, arguments)
      },
      finishPullDown() {
        this.$refs.refreshScroll && this.$refs.refreshScroll.finishPullDown.apply(this.$refs.refreshScroll, arguments)
      },
      finishpullUp() {
        this.$refs.refreshScroll && this.$refs.refreshScroll.finishpullUp.apply(this.$refs.refreshScroll, arguments)
      },
      loading() {
        this.$emit("loading")
      },
      loadMore() {
        this.$emit("loadMore")
      }
    }
  }
</script>

<style scoped>

</style>

```
### 4、提供刷新的样式-带图标的

```vue
<template>
  <cpcBaseRefresh ref="refreshScroll" @loading="loading" @loadMore="loadMore">
    <div slot="statePulldown">
      <i class="iconfont icon-down-arrow"></i>
      下拉刷新
    </div>
    <div slot="stateRelease">
      <i class="iconfont icon-refreshup"></i>
      释放刷新
    </div>
    <div slot="stateRefreshing">
      <loading2></loading2>
      刷新中
      <morePoint></morePoint>
    </div>
    <div slot="stateRefreshEnd">
      <finishedTick :isShow="true"></finishedTick>
      刷新完成
    </div>
    <slot></slot>
    <div slot="loadMoreing">
      <loading2></loading2>
      加载中
      <morePoint></morePoint>
    </div>
    <div slot="loadMores">加载更多</div>
    <div slot="loadMoreALL">加载全部了</div>
  </cpcBaseRefresh>
</template>

<script>
  import cpcBaseRefresh from '../../refresh/cpcBaseRefresh.vue'
  import loading2 from '../../../animate/loading/loading2.vue';
  import finishedTick from '../../../animate/finishedTick/finishedTick.vue';
  import morePoint from '../../../animate/morePoint/morePoint.vue';

  export default {
    components: {cpcBaseRefresh, loading2,finishedTick,morePoint},
    data() {
      return {}
    },
    methods: {
      setLoadMoreALL() {
        this.$refs.refreshScroll && this.$refs.refreshScroll.setLoadMoreALL.apply(this.$refs.refreshScroll, arguments)
      },
      finishPullDown() {
        this.$refs.refreshScroll && this.$refs.refreshScroll.finishPullDown.apply(this.$refs.refreshScroll, arguments)
      },
      finishpullUp() {
        this.$refs.refreshScroll && this.$refs.refreshScroll.finishpullUp.apply(this.$refs.refreshScroll, arguments)
      },
      loading() {
        this.$emit("loading")
      },
      loadMore() {
        this.$emit("loadMore")
      }
    }
  }
</script>

<style scoped>

</style>

```

### 5、基于better-scroll的封装的轮播图
[示例代码](/zh-cn/betterScroll/example?id=_4%e3%80%81%e8%bd%ae%e6%92%ad%e5%9b%be%e7%9a%84%e7%a4%ba%e4%be%8b)
```vue
<template>
  <div class="slider" ref="slider">
    <div class="slider-group" ref="sliderGroup">
      <slot>
      </slot>
    </div>
    <div class="dots">
      <span class="dot" :class="{active: currentPageIndex+1 === index }" v-for="(item, index) in dots"></span>
    </div>
  </div>
</template>

<script>
  import {addClass} from '../../../utils/dom'
  import BScroll from 'better-scroll'
  export default{
    data() {
      return {
        dots:[],
        currentPageIndex: -1
      }
    },
    props:{
      loop:{
        type:Boolean,
        default:true
      },
      autoPlay:{
        type:Boolean,
        default:true
      },
      interval:{
        type: Number,
        default:4000
      }
    },
    mounted() {

      this._setSliderWidth()
      setTimeout(() => {
        // 在初始化slider前初始化dot
        this._initDots()
        this._initSlider()
        if (this.autoPlay) {
          this._play()
        }
      }, 20)
      // 监听窗口大小改变时间
      window.addEventListener('resize', () => {
        if (!this.slider) {
          return
        }
        this._setSliderWidth(true)
        this.slider.refresh()
      })
    },
    methods:{
      _setSliderWidth(isResize) {
        this.children = this.$refs.sliderGroup.children
        let width = 0
        // slider 可见宽度
        let sliderWidth = this.$refs.slider.clientWidth
        for (let i = 0; i < this.children.length; i++) {
          let child = this.children[i]
          // 设置每个子元素的样式及高度
          addClass(child, 'slider-item')
          child.style.width = sliderWidth + 'px'
          // 计算总宽度
          width += sliderWidth
        }
        // 循环播放首尾各加一个,因此总宽度还要加两倍的宽度
        if (this.loop && !isResize) {
          width += 2 * sliderWidth
        }
        this.$refs.sliderGroup.style.width = width + 'px'
      },
      _initSlider() {
        this.slider = new BScroll(this.$refs.slider, {
          click: true,
          scrollX: true,
          scrollY: false,
          momentum: false,
          snap: {
            loop: true,
            threshold: 0.3,
            speed: 400
          },
        })
        // 监听滚动结束时间获取pageX
        this.slider.on('scrollEnd', () => {
          let pageIndex = this.slider.getCurrentPage().pageX
          if (this.loop) {
            // 由于bscroll循环播放首尾各加一个,因此索引-1
            pageIndex -= 1
          }
          this.currentPageIndex = pageIndex
          if (this.autoPlay) {
            this._play()
          }
        })
        this.slider.on('beforeScrollStart', () => {
          if (this.autoPlay) {
            clearTimeout(this.timer)
          }
        })
      },
      _initDots() {
        // 长度为n的空数组
        this.dots = new Array(this.children.length)
      },
      _play() {
        // currentPageIndex为不含首尾副本的索引，因此若有循环要+2
        let pageIndex = this.currentPageIndex + 1
        if (this.loop) {
          pageIndex += 1
        }
        this.timer = setTimeout(() => {
          this.slider.goToPage(pageIndex, 0, 400)
        }, this.interval)
      }
    },
    // 生命周期destroyed销毁清除定时器，有利于内存释放
    destroyed() {
      clearTimeout(this.timer)
    },
  }
</script>
<style scoped>
  .slider{
    min-height: 1px;
    position: relative;
    overflow: hidden;
  }

  .slider-group{
    position: relative;
    overflow: hidden;
    white-space: nowrap;
  }

  .slider-item{
    float: left;
    box-sizing: border-box;
    overflow: hidden;
    text-align: center;
    height: 150px;
    overflow: hidden;
  }

  .slider-item a{
    display: block;
    width: 100%;
    overflow: hidden;
    text-decoration: none;
  }


  .slider-item img{
    display: block;
    width: 100%;
  }

  .dots{
    position: absolute;
    right: 0;
    left: 0;
    bottom: 12px;
    text-align: center;
    font-size: 0;
  }

  .dot{
    display: inline-block;
    margin: 0 4px;
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: red;
  }

  .active{
    width: 20px;
    border-radius: 5px;
  }
</style>

```
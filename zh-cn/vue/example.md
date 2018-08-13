<div style='background: #000 url("/images/honor7x.jpg");
                  width: 360px;
                  height: 730px;
                  -webkit-background-size: 100%;
                  background-size: 100%;
                  position: fixed;
                  top: 80px;
                  right: 20px;'>
  <iframe style='auto;width: 320px;height: 645px;position: absolute;top: 30px;left: 20px;' name="vueExample" src="../../myApp/index.html#/cpcBaseScroll" frameborder="0" scrolling="auto" width="360px" height="500px"></iframe>
</div>

## 基础应用
### 1、卡片(card)
<a href="../../myApp/index.html#/card" target="vueExample" >效果展示</a>

```vue
<template>
  <cpcBackHeadAndScroll title="卡片">
    <cpcSingleRow1 :datas="rows.row1"></cpcSingleRow1>
    <br>
    <cpcSingleRow2 :datas="rows.row2"></cpcSingleRow2>
    <br>
    <cpcSingleRow3 :datas="rows.row3"></cpcSingleRow3>
    <br>
    <cpcSingleRow4></cpcSingleRow4>
  </cpcBackHeadAndScroll>
</template>

<script type="text/ecmascript-6">
  import cpcBackHeadAndScroll from '../../../CPCUI/scroll/headAndScroll/cpcBackHeadAndScroll.vue'
  import cpcSingleRow1 from '../../../CPCUI/cards/singleRow/type/cpcSingleRow1.vue'
  import cpcSingleRow2 from '../../../CPCUI/cards/singleRow/type/cpcSingleRow2.vue'
  import cpcSingleRow3 from '../../../CPCUI/cards/singleRow/type/cpcSingleRow3.vue'
  import cpcSingleRow4 from '../../../CPCUI/cards/singleRow/type/cpcSingleRow4.vue'

  export default {
    components: {cpcBackHeadAndScroll, cpcSingleRow1, cpcSingleRow2, cpcSingleRow3, cpcSingleRow4},
    data() {
      return {
        rows: {
          row1: {
            img: "./static/images/logo.png",
            title: "标题标题标题标题标题标题标题标题",
            describe: "我是描述的内容",
            sellingPrice: 420,
            realPrice: "原价500",
            right: "竞价成功"
          },
          row2: {
            img: "./static/images/logo.png",
            title: "标题标题标题标题标题标题标题标题",
            describe: "描述内容描述内容描述内容描述内容描述内容描述内容描述内容描述内容描述内容描述内容描述内容描述内容描述内容描述内容",
            sellingPrice: 420,
            realPrice: "原价500",
            right: "竞价成功"
          },
          row3: {
            img: "./static/images/logo.png",
            title: "标题标题标题标题标题标题标题标题",
            sellingPrice:"¥500",
            realPrice:"抢购价¥350",
            buy:"立即购买",
          }
        }
      }
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


### 2、头部栏(topNav)
<a href="../../myApp/index.html#/topNav" target="vueExample" >效果展示</a>
```vue
<template>
    <backHeadAndScroll title="头部栏目">
      <cpcTopNavType1 title="标题" rightTxt="更多"></cpcTopNavType1>
      <cpcTopNavType2 title="标题"></cpcTopNavType2>
    </backHeadAndScroll>
</template>

<script type="text/ecmascript-6">
  import backHeadAndScroll from '../../../CPCUI/scroll/headAndScroll/cpcBackHeadAndScroll.vue'
  import cpcTopNavType1 from '../../../CPCUI/topNav/type/cpcTopNavType1.vue';
  import cpcTopNavType2 from '../../../CPCUI/topNav/type/cpcTopNavType2.vue';
    export default {
        components: {cpcTopNavType1,cpcTopNavType2,backHeadAndScroll},
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

### 2、吐司(toast)
<a href="../../myApp/index.html#/toast" target="vueExample" >效果展示</a>
```vue
<template>
  <backHeadAndScroll title="吐司">
    <button @click="ToastClick">toast1</button>
  </backHeadAndScroll>
</template>

<script type="text/ecmascript-6">
  import backHeadAndScroll from '../../../CPCUI/scroll/headAndScroll/cpcBackHeadAndScroll.vue'

  export default {
    components: {backHeadAndScroll},
    data() {
      return {}
    },
    props: {},
    methods: {
      ToastClick() {
        this.$toast("我是吐司");
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
>需要在main.js中注册使用

```javascript
import cpcBaseToast from './CPCUI/toast/cpcBaseToast'
Vue.use(cpcBaseToast);
```


### 2、轮播图(banner)
<a href="../../myApp/index.html#/banner" target="vueExample" >效果展示</a>
```vue
<template>
  <cpcBackHeadAndScroll title="轮播图">
    <p style="">better-scroll 封装的</p>
    <cpcBanner1>
      <img v-for='item in slider' width="100%" height="100%" :src="item.img" alt="">
    </cpcBanner1>
    <p style="">swiper 图片导航</p>
    <cpcBanner2></cpcBanner2>
    <p style="">swiper什么都不配置</p>
    <baseBanner :datas="slider"></baseBanner>
    <p>从右向左运动</p>
    <baseBanner dir="rtl" :datas="slider"></baseBanner>
    <p style="">swiper 不循环同时使用动态点指示器</p>
    <baseBanner dynamicBullets :loop="false" :datas="slider"></baseBanner>
    <p style="">swiper 淡入淡出方式</p>
    <baseBanner effect="fade" :datas="slider"></baseBanner>
    <p style="">swiper 方块</p>
    <baseBanner effect="cube" :datas="slider"></baseBanner>
    <p style="">swiper 3d流</p>
    <baseBanner effect="coverflow" :datas="slider"></baseBanner>
    <p style="">swiper 3d翻转</p>
    <baseBanner effect="flip"  :datas="slider"></baseBanner>
    <p style="">swiper 对其方式</p>
    <baseBanner dotAlign="left" :datas="slider"></baseBanner>
    <baseBanner dotAlign="right" :datas="slider"></baseBanner>
    <p style="">swiper 指示器</p>
    <baseBanner :datas="slider"></baseBanner>
    <baseBanner dotType="fraction" :datas="slider"></baseBanner>
    <baseBanner dotType="progressbar" :datas="slider"></baseBanner>
    <p style="">swiper 同时展示的个数和之间的间距</p>
    <baseBanner :slidesPerView="2" :datas="slider"></baseBanner>
    <baseBanner :spaceBetween="30" :datas="slider"></baseBanner>
    <baseBanner :slidesPerView="2" :spaceBetween="30" :datas="slider"></baseBanner>
    <p>垂直banner</p>
    <baseBanner direction="vertical" :datas="slider"></baseBanner>
  </cpcBackHeadAndScroll>
</template>

<script type="text/ecmascript-6">
  import cpcBackHeadAndScroll from '../../../CPCUI/scroll/headAndScroll/cpcBackHeadAndScroll.vue'
  import cpcBanner1 from '../../../CPCUI/banner/type/cpcBanner1.vue'
  import cpcBanner2 from '../../../CPCUI/banner/type/cpcBanner2.vue'
  import baseBanner from '../../../CPCUI/banner/baseBanner.vue'

  export default {
    components: {cpcBackHeadAndScroll, cpcBanner1, cpcBanner2,baseBanner},
    data() {
      return {
        slider: [
          {
            img: "./static/images/img1.jpg",
            url: "/"
          },
          {
            img: "./static/images/img4.jpg",
            url: "/"
          },
          {
            img: "./static/images/img3.jpg",
            url: "/"
          },
          {
            img: "./static/images/img2.jpg",
            url: "/"
          },
          {
            img: "./static/images/img1.jpg",
            url: "/"
          },
          {
            img: "./static/images/img0.jpg",
            url: "/"
          },
          {
            url: "/",
            img: "./static/images/banner1.jpg"
          },
          {
            url: "/",
            img: './static/images/banner2.jpg'
          },
          {
            url: "/",
            img: "./static/images/banner3.jpg"
          },
          {
            url: "/",
            img: './static/images/honor7x.jpg'
          },

        ],
      }
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
  p {
    background-color: red;
    text-align: center;
  }
</style>
<style lang="less">
  #banner {
    .swiper-pagination-bullet {
      opacity: 1;
      background-color: #fff;
    }
    .swiper-pagination-bullet-active {
      background-color: #E02E24;
    }

  }
</style>
```

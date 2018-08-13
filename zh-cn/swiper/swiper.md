#swiper的使用
## 1、安装swiper的依赖包
```sh
 npm install vue-awesome-swiper --save
```
## 2、在main中配置到如下:
```javascript
    import VueAwesomeSwiper from 'vue-awesome-swiper'
    // require styles
    import 'swiper/dist/css/swiper.css'
    Vue.use(VueAwesomeSwiper, /* { default global options } */)
```

[demo示例网址](https://surmon-china.github.io/vue-awesome-swiper/)

## 3、轮播图的封装


```shell
<template>
  <swiper :dir="dir" id="banner" ref="swiper" :options="getOpeions">
    <swiper-slide v-for="item in datas">
      <img class="bannerImg" :src="item.img" :data-bindurl="item.url">
    </swiper-slide>
    <div :style="{'text-align': dotAlign}" class="swiper-pagination" slot="pagination"></div>
  </swiper>
</template>

<script type="text/ecmascript-6">
  export default {
    components: {},
    data() {
      return {}
    },
    props: {
      datas:{
        type:Array,
        default:[]
      },
      /*ltr:代表左到右的排列方式,rtl:代表右到左的排列方式*/
      dir:{
        type:String,
        default:"ltr"
      },
      /*设置水平(horizontal)或垂直(vertical)*/
      direction:{
        type:String,
        default:'horizontal'
      },
      /* 切换效果
        "slide"（位移切换），可设置为'slide'（普通切换、默认）,
        "fade"（淡入）
        "cube"（方块）
        "coverflow"（3d流）
        "flip"（3d翻转）
      */
      effect: {
        type: String,
        default: "slide"
      },
      /* 轮播间隔时间 */
      delay:{
        type:Number,
        default:3000
      },
      /* 允许用户点击点，却换到当前page页面 */
      clickable:{
        type:Boolean,
        default:false
      },
      /*用户操作swiper之后，是否禁止autoplay*/
      disableOnInteraction:{
        type:Boolean,
        default:false
      },
      /*是否开启循环*/
      loop:{
        type:Boolean,
        default:true
      },
      /*动态点指示器*/
      dynamicBullets:{
        type:Boolean,
        default:false
      },
      /*
        ‘bullets’  圆点（默认）
        ‘fraction’  分式
        ‘progressbar’  进度条
      */
      dotType:{
        type:String,
        default:'bullets'
      },
      /*指示器的对齐方式：left center right*/
      dotAlign:{
        type:String,
        default:"center"
      },
      /*同时显示的个数,可以是数值或者auto*/
      slidesPerView:{
        type:[Number,String],
        default:1
      },
      /*每个之间项之间的距离*/
      spaceBetween:{
        type:Number,
        default:0
      },
      /*设定为true时，active slide会居中，而不是默认状态下的居左*/
      centeredSlides:{
        type:Boolean,
        default:false
      },
      /*slide滑动时只滑动一格，并自动贴合wrapper，设置为true则变为free模式，slide会根据惯性滑动可能不止一格且不会贴合。*/
      freeMode:{
        type:Boolean,
        default:false
      },
    },
    methods: {
      changeActive(e) {
        let url = e.target.dataset.bindurl;
        this.$router.push(url)
      }
    },
    computed: {
      getOpeions() {
        let options = {
          effect: this.effect,
          autoplay: {
            delay: this.delay,
            disableOnInteraction: this.disableOnInteraction
          },
          on: {
            tap: this.changeActive
          },
          freeMode:this.freeMode,
          centeredSlides: this.centeredSlides,
          direction:this.direction,
          loop:this.loop,
          slidesPerView: this.slidesPerView,
          spaceBetween: this.spaceBetween,
          pagination: {
            el: '.swiper-pagination',
            clickable: this.clickable,
            dynamicBullets: this.dynamicBullets,
            type: this.dotType,
          }
        }
        return options;
      }
    },
    mounted() {

    },
    destroyed() {

    }
  }
</script>

<style lang="less" scoped>
  #banner {
    background-color: #fff;
    height: 1.5rem;
    .swiper-pagination {
      padding-right: 0.1rem;
    }
    .bannerImg {
      width: 100%;
      height: 1.5rem;
    }
  }
</style>

```

`baseBanner`的props
<table style="width:100%;text-align:center;">
    <tr>
        <th width="10%">参数名称</th>
        <th  width="60%">说明</th>
        <th  width="20%">类型</th>
        <th  width="10%">默认值</th>
    </tr>
     <tr>
       <td>datas</td>
       <td>轮播图的数据格式如下：<br>
       [
         {img: "./static/images/img1.jpg",url: "/"},<br>
         {img: "./static/images/img4.jpg",url: "/"}
       ]
       </td>
       <td>Array</td>
       <td>[]</td>
     </tr>
     <tr>
        <td>dir</td>
        <td>ltr:代表左到右的排列方式,rtl:代表右到左的排列方式</td>
        <td>String</td>
        <td>ltr</td>
    </tr>
    <tr>
        <td>direction</td>
        <td>设置水平(horizontal)或垂直(vertical)</td>
        <td>String</td>
        <td>horizontal</td>
    </tr>
    <tr>
        <td>effect</td>
        <td>"slide"（位移切换），可设置为'slide'（普通切换、默认）,
                    "fade"（淡入）
                    "cube"（方块）
                    "coverflow"（3d流）
                    "flip"（3d翻转）
         </td>
        <td>String</td>
        <td>slide</td>
    </tr>
    <tr>
        <td>delay</td>
        <td>轮播间隔时间</td>
        <td>Number</td>
        <td>3000</td>
    </tr>
    <tr>
        <td>clickable</td>
        <td>允许用户点击点，却换到当前page页面</td>
        <td>Boolean</td>
        <td>false</td>
    </tr>
    <tr>
        <td>disableOnInteraction</td>
        <td>用户操作swiper之后，是否禁止autoplay</td>
        <td>Boolean</td>
        <td>false</td>
    </tr>
    <tr>
        <td>loop</td>
        <td>是否开启循环</td>
        <td>Boolean</td>
        <td>true</td>
    </tr>
    <tr>
        <td>dynamicBullets</td>
        <td>动态点指示器</td>
        <td>Boolean</td>
        <td>false</td>
    </tr>
    <tr>
        <td>dotType</td>
        <td> ‘bullets’  圆点（默认）
                    ‘fraction’  分式
                    ‘progressbar’  进度条</td>
        <td>String</td>
        <td>bullets</td>
    </tr>
    <tr>
        <td>dotAlign</td>
        <td>指示器的对齐方式：left center right</td>
        <td>String</td>
        <td>center</td>
    </tr>
    <tr>
        <td>slidesPerView</td>
        <td>同时显示的个数,可以是数值或者auto</td>
        <td>[Number,String]</td>
        <td>1</td>
    </tr>
    <tr>
        <td>spaceBetween</td>
        <td>每个之间项之间的距离</td>
        <td>Number</td>
        <td>0</td>
    </tr>
    <tr>
        <td>centeredSlides</td>
        <td>设定为true时，active slide会居中，而不是默认状态下的居左</td>
        <td>Boolean</td>
        <td>false</td>
    </tr>
    <tr>
        <td>freeMode</td>
        <td>slide滑动时只滑动一格，并自动贴合wrapper，设置为true则变为free模式，slide会根据惯性滑动可能不止一格且不会贴合。</td>
        <td>Boolean</td>
        <td>false</td>
    </tr>
</table>
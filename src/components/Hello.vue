<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <swiper class="swiper-container" id="topNav" :options="swiperOption" ref="mySwiper">
        <swiper-slide v-for="(tab,index) in tabs" :class="{active:thisIndex==index}"><span>{{tab}}</span></swiper-slide>
    </swiper>
<!-- Swiper -->
    <swiper class="swiper-container gallery-top" :options="slideSwiper" ref="mySlide">
        <swiper-slide v-for='content in contents'>{{content}}</swiper-slide>
    </swiper>
  </div>
</template>

<script>
require('../assets/swiper.min.css')
export default {
  name: 'hello',
  data () {
    return {
      thisIndex:0,
      tabs:['推荐','热点','深圳','视频','社会','娱乐','科技','问答','汽车','财经'],
      contents:['推荐内容','热点内容','深圳内容','视频内容','社会内容','娱乐内容','科技内容','问答内容','汽车内容','财经内容'],
      swiperOption: {
          freeMode: true,
          slidesPerView: 'auto',
          onTap: mySwiper => {
            this.thisIndex=mySwiper.clickedIndex
            this.slideShow(mySwiper.clickedIndex,'active');
            // this.slide.slideTo(mySwiper.clickedIndex, 1000, false)
            // this.swiperTab.slideTo(mySwiper.clickedIndex, 1000, false)
          }
        },
      slideSwiper:{
        speed:500,
        freeMode: false,
        onSlideChangeStart: mySwiper => {
          this.thisIndex=mySwiper.realIndex
            this.slideShow(mySwiper.realIndex,'active');
            // this.swiperTab.slideTo(mySwiper.realIndex, 1000, false)
        }
      },
      msg: 'Welcome to Your Vue.js App'
    }
  },
  computed: {
      swiperTab() {
        return this.$refs.mySwiper.swiper
      },
      slide(){
        return this.$refs.mySlide.swiper
      }
    },
    methods:{
      slideShow(tabIndex,active){
        var selfTab=this.swiperTab;
        var swiperWidth = selfTab.container[0].clientWidth 
        var maxTranslate = selfTab.maxTranslate(); 
        var maxWidth = -maxTranslate + swiperWidth / 2 
        var slideLeft = selfTab.slides[tabIndex].offsetLeft
        var slideWidth = selfTab.slides[tabIndex].clientWidth
        var slideCenter = slideLeft + slideWidth / 2
        this.slide.slideTo(tabIndex, 500, false);
          // 被点击slide的中心点
          selfTab.setWrapperTransition(300)
          if (slideCenter < swiperWidth / 2) {
              selfTab.setWrapperTranslate(0)
          } else if (slideCenter > maxWidth) {
             selfTab.setWrapperTranslate(maxTranslate)
          } else {
              var nowTlanslate = slideCenter - swiperWidth / 2
              selfTab.setWrapperTranslate(-nowTlanslate)
          }
          this.thisIndex=tabIndex
      }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
html, body {
        position: relative;
        height: 100%;
    }
    body {
        font-family: Helvetica Neue, Helvetica, Arial, sans-serif;
        font-size: 14px;
        margin: 0;
        padding: 0;
    }
    .gallery-top.swiper-container {
        width: 100%;
        height: 300px;
        margin-left: auto;
        margin-right: auto;
    }
    .gallery-top .swiper-slide {
        background: #eee;
        background-size: cover;
        background-position: center;
    }
    .gallery-top {
        height: 80%;
        width: 100%;
    }
    .gallery-thumbs {
        height: 20%;
        box-sizing: border-box;
        padding: 10px 0;
    }
    .gallery-thumbs .swiper-slide {
        width: 25%;
        height: 100%;
        opacity: 0.4;
    }
    .gallery-thumbs .swiper-slide-active {
        opacity: 1;
    }
    #topNav {
        width: 100%;
        overflow: hidden;
        font: 16px/32px hiragino sans gb, microsoft yahei, simsun;
        border-bottom:1px solid #f8f8f8;
        background: #fff;
    }
    #topNav .swiper-slide {
      width: 60px!important;
      padding: 0 5px;
      letter-spacing:2px;
      text-align:center;
    }
    #topNav .swiper-slide span{

        transition:all .3s ease;
        display:block;
    }
    #topNav .active span{
        transform:scale(1.1);
        color:#FF2D2D;
    }
</style>

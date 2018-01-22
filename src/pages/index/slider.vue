<template>
  <swiper class="banner index-banner" :options="swiperOption" v-if="sliders.length">
    <swiper-slide v-for="item of sliders" :key="item.id">
      <img class="banner-img" :src="item.imgUrl"/>
    </swiper-slide>
    <div class="swiper-pagination"  slot="pagination"></div>
  </swiper>
</template>

<script>
export default {
  name: 'index-slider',
  props: {
    sliders: Array
  },
  data () {
    return {
      swiperOption: {
        loop: true,
        pagination: '.swiper-pagination',
        autoplay: 3000,
        autoplayDisableOnInteraction: false
      }
    }
  }
}
</script>

<style lang="stylus" scoped>
  @import '../../assets/common/varibles.styl'
  .banner
    overflow hidden
    height 0
    padding-bottom 31.25%
    width 100%
    .banner-img
      width 100%
</style>

<style lang="stylus">
  .index-banner
    .swiper-pagination-bullet
      background #fff
</style>

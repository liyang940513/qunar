<template>
  <swiper class="icons" :options="swiperOption" v-if="icons.length">
    <swiper-slide class="icon-page"
                  v-for="(page, index) of pages" :key="index">
      <div class="icons-list">
        <div v-for="item in page" :key="item.id" class="icons-item">
          <img class="icon-img" :src="item.imgUrl">
          <p class="icons-title">{{item.title}}</p>
        </div>
      </div>
    </swiper-slide>
    <div class="swiper-pagination"  slot="pagination"></div>
  </swiper>
</template>

<script>
export default {
  name: 'index-icons',
  props: {
    icons: Array
  },
  data () {
    return {
      swiperOption: {
        pagination: '.swiper-pagination'
      }
    }
  },
  computed: {
    pages () {
      const pages = []
      this.icons.forEach((value, index) => {
        const page = Math.floor(index / 8)
        if (!pages[page]) {
          pages[page] = []
        }
        pages[page].push(value)
      })
      return pages
    }
  }
}
</script>

<style lang="stylus" scoped>
  @import '../../assets/common/varibles.styl'
  .icons >>> .swiper-pagination-bullet
    background $bgColor
  .icons
    width 100%
    overflow hidden
    height 0
    padding-bottom 3.4rem
    .icons-list
      display flex
      flex-wrap wrap
      .icons-item
        width 25%
        padding-top .3rem
        text-align center
        .icon-img
          width .66rem
          height .66rem
        .icons-title
          overflow hidden
          text-overflow ellipsis
          white-space nowrap
          margin-top .16rem
          font-size .28rem
          color #333
</style>

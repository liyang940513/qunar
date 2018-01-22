<template>
  <div class="main">
    <index-header></index-header>
    <index-slider :sliders="sliders"></index-slider>
    <index-icons :icons="icons"></index-icons>
    <index-scroller class="scroller" :sights="sights"></index-scroller>
  </div>
</template>

<script>
import axios from 'axios'
import { mapState, mapMutations } from 'vuex'

import IndexHeader from './header'
import IndexSlider from './slider'
import IndexIcons from './icons'
import IndexScroller from './scroller'

export default {
  name: 'index',
  data () {
    return {
      sliders: [],
      icons: [],
      sights: []
    }
  },
  components: {
    IndexHeader,
    IndexSlider,
    IndexIcons,
    IndexScroller
  },
  computed: {
    ...mapState(['city'])
  },
  methods: {
    ...mapMutations(['changeCity']),
    getIndexData () {
      axios.get('/api/index.json?city=' + this.city)
        .then(this.handleDataSucc.bind(this))
        .catch(this.handleDataError.bind(this))
    },
    handleDataSucc (res) {
      res = res ? res.data : null
      if (res && res.ret && res.data) {
        res.data.city && (this.changeCity(res.data.city))
        res.data.slider && (this.sliders = res.data.slider)
        res.data.icons && (this.icons = res.data.icons)
        res.data.sights && (this.sights = res.data.sights)
      } else {
        this.handleDataError()
      }
    },
    handleDataError () {
      console.log('error')
    }
  },
  mounted () {
    this.getIndexData()
  }
}
</script>

<style scoped lang="stylus">
  .main
    display flex
    flex-direction column
    position absolute
    left 0
    right 0
    bottom 0
    top 0
    .scroller
      flex 1
      overflow hidden
</style>

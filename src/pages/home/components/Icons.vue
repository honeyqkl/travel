<template>
  <div class="icons">
    <swiper :options="swiperOption">
      <swiper-slide v-for="(page , index) of pages" :key="index">
        <div class="icon" v-for="item of page" :key="item.id">
          <div class="icon-img">
            <img class="icon-img-content" :src="item.imgUrl" alt="">
          </div>
          <p class="icon-desc">{{item.desc}}</p>
        </div>
      </swiper-slide>
    </swiper>
  </div>
</template>
<script>
export default {
  name: 'HomeIcons',
  props: {
    list: Array
  },
  data () {
    return {
      swiperOption: {
        autoplay: false
      }
    }
  },
  computed: {
    pages: function () {
      const pages = []
      this.list.forEach((item, index) => {
        // item在第几页记录在了page中 生成一个二维数组
        const page = Math.floor(index / 8)
        if (!pages[page]) {
          pages[page] = []
        }
        pages[page].push(item)
      })
      return pages
    }
  }
}
</script>
<style lang="stylus" scoped>
  @import "~styles/varibles.styl"
  @import "~styles/mixins.styl"
  .icons >>> .swiper-container
    height: 0
    padding-bottom :50%
  .icons
    margin-top: .1rem
    .icon
      position: relative
      overflow: hidden
      float: left
      height: 0
      width: 25%
      padding-bottom: 25%

      .icon-img
        position: absolute
        top: 0
        left: 0
        right: 0
        box-sizing: border-box
        bottom: 0.44rem
        padding: .1rem

        .icon-img-content
          height: 100%
          margin: 0 auto
          display: block

      .icon-desc
        position: absolute
        left: 0
        right: 0
        bottom: 0
        text-align: center
        height: .44rem
        line-height: .44rem
        color: $darkTextColor
        ellipsis()
</style>

<template>
	<div class="icons">
    <swiper :options="swiperOptionIcon">
      <swiper-slide v-for="(page , index) of pages" :key="index">
        <div class="icon" v-for="item of page" :key="item.id">
          <div class="icon-img" >
            <img class="icon-img-content" :src='item.imgUrl' />
          </div>
          <p class="icon-desc">{{item.desc}}</p>
        </div>
      </swiper-slide>
      <div class="swiper-pagination" slot="pagination"></div>
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
        swiperOptionIcon: {
          pagination: ".swiper-pagination",
          autoplay: false,
        }
      }
    },
    computed: {
      pages () {
        const pages = []
        this.list.forEach((item, index) => {
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
  @import '~styles/varibles.styl'
  @import '~styles/mixins.styl'
	.icons >>> .swiper-container
    height: 0
    padding-bottom: 56%
  .icons >>> .swiper-pagination-bullet
    background: #000
    opacity: .4
  .icons >>> .swiper-pagination-bullet-active 
    background: #007aff
    opacity: 1
  .icon
    overflow: hidden
    position: relative
    float: left
    width: 25%
    height: 0
    padding-bottom: 25%
    .icon-img 
      position: absolute
      top: .2rem
      left: 0
      right: 0
      bottom: .44rem
      .icon-img-content 
        display: block
        margin: 0 auto
        height: 100%
    .icon-desc 
      position: absolute
      left: 0
      right: 0
      bottom: 0
      height: .44rem
      line-height: .44rem
      text-align: center
      color: $darkTextColor
      ellipsis()
</style>

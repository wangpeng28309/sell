<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
      	<img width="64" height="64" :src="seller.avatar">
      </div>
      <div class="content">
      	<div class="title">
      		<span class="brand"></span>
      		<span class="name">{{seller.name}}</span>
      	</div>
      	<div class="description">
      	  {{seller.description}}/{{seller.deliveryTime}}分钟送达
      	</div>
      	<div v-if="seller.supports" class="support">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div v-if="seller.supports" class="support-count">
        <span class="count">{{seller.supports.length}}个</span>
        <span class="icon-keyboard_arrow_right" @click="showDetail"></span>
      </div>
    </div>  
    <div class="bulletin-wrapper">
      <span class="bulletin-title"></span>
      <span class="bulletin-text">{{seller.bulletin}}</span>
    </div>
    <div class="background">
      <img :src="seller.avatar" width="100%" height="100%">
    </div>
    <div v-show="detailShow" class="detail">
      <div class="detail-wrapper clearfix">
        <div class="detail-main">
        <h1 class="name">{{seller.name}}</h1>
        <star :size="36" :score="seller.score"></star>
        <h2 class="text">优惠信息</h2>
        <ul v-if="seller.supports" class="supports">
          <li class="support-item" v-for="(item, index) in seller.supports">
            <span class="icon" :class="classMap[seller.supports[index].type]"></span>
            <span class="">{{seller.supports[index].description}}</span>
          </li>
        </ul>
        <h2 class="text">商家公告</h2>
        <div class="">{{seller.bulletin}}</div>
        </div>
      </div>
      <div class="detail-close">
        <span class="icon-close" @click="hideDetail"></span>
      </div>
    </div>
  </div>
</template>

<script>
import star from '../star/star.vue'
export default {
  name: 'header',
  components: {
    star
  },
  props: {
    seller: {
      type: Object
    }
  },
  data () {
    return {
      detailShow: false
    }
  },
  methods: {
    showDetail () {
      this.detailShow = true
    },
    hideDetail () {
      this.detailShow = false
    }
  },
  created () {
    this.classMap = ['decrease', 'discount', 'guarantee', 'invoice', 'special']
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
  @import "../../common/stylus/mixin";
  .header
    position: relative
    background: rgba(7, 17, 27, 0.5)
    overflow: hidden
    color: #fff
    .content-wrapper
      position: relative
      padding: 24px 12px 18px 24px
      .avatar
        display: inline-block
        margin-left: 0 
      .content
        display:inline-block
        .title
          margin: 2px 0 8px 0
          .brand
            display: inline-block
            vertical-align: top
            width: 30px
            height: 18px
            bg-image('brand')
            background-size: 30px 18px
            background-repeat: no-repeat
          .name
            margin-left: 6px
            font-size: 16px
            line-height: 18px
            font-weight: bold
        .support
          .icon
            display: inline-block
            width: 12px
            height: 12px
            margin-right: 4px
            background-size: 12px 12px
            background-repeat:no-repeat
            &.decrease
              bg-image('decrease_1')
            &.discount
              bg-image('discount_1')
            &.guarantee
              bg-image('guarantee_1')
            &.invoice
              bg-image('invoice_1')
            &.special
              bg-image('special_1')
      .support-count
        position: absolute
        right: 12px
        bottom: 18px
    .bulletin-wrapper
      overflow: hidden
      white-space: nowrap
      text-overflow: ellipsis
    .background
      position: absolute
      top: 0
      left: 0
      width: 100%
      height: 100%
      z-index: -1
      filter: blur(10px)
    .detail
      position: fixed
      z-index: 100
      background: rgba(7, 17, 27, 0.8)
      overflow: auto
      width: 100%
      height: 100%
      top: 0
    .detail-wrapper
      min-height: 100%
      .detail-main
        margin-top: 64px
        padding-bottom: 64px
        .name
        .supports
          .icon
            display: inline-block
            width: 16px
            height: 16px
            vertical-align: top
            margin-right: 6px
            background-size: 16px 16px
            background-repeat: no-repeat
            &.decrease
              bg-image('decrease_2')
            &.discount
              bg-image('discount_2')
            &.guarantee
              bg-image('guarantee_2')
            &.invoice
              bg-image('invoice_2')
            &.special
              bg-image('special_2')
    .detail-close
      position: relative
      width: 32px
      height: 32px
      margin: -64px auto 0 auto
      clear: both
      font-size: 32px
</style>

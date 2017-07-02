<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
      	<img width="64" height="64" v-bind:src="seller.avatar">
      </div>
      <div class="content">
      	<div class="title">
      		<span class="brand"></span>
      		<span class="name">{{seller.name}}</span>
      	</div>
      	<div class="description">
      	  {{seller.description}}/{{seller.deliveryTime}}分钟送达
      	</div>
      	<div v-if="seller.support" class="support">
      	  <span class="icon"></span>
      	  <span class="text">
      	  	{{seller.support[0].description}}
      	  </span>
      	</div>
      </div>
      <div v-if="seller.supports" class="support-count">
        <span class="count">{{seller.supports.length}}个</span>
        <span class="icon-keyboard_arrow_right"></span>
      </div>
    </div>  
    <div class="bulletin-wrapper">
      <span class="bulletin-title"></span>
      <span class="bulletin-text" @click="showDetail">{{seller.bulletin}}</span>
    </div>
    <div class="background">
      <img v-bind:src="seller.avatar" width="100%" height="100%">
    </div>
    <div v-show="detailShow" class="detail">
      <div class="detail-wrapper clearfix">
        <div class="detail-main">
          <p>{{seller.bulletin}}</p>
        </div>
      </div>
      <div class="detail-close">
        <span class="icon-close"></span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'header',
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
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
  .header
    position: relative
    background: rgba(7, 17, 27, 0.5)
    overflow: hidden
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
    .detail-close
      position: relative
      width: 32px
      height: 32px
      margin: -64px auto 0 auto
      clear: both
      font-size: 32px
</style>

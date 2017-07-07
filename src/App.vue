<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="title">
      <div class="title-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="title-item">
        <router-link to="/ratings">评论</router-link>
      </div>
      <div class="title-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <keep-alive>
      <router-view :seller="seller"></router-view>
    </keep-alive>
    <div class="bottom"></div>
  </div>
</template>

<script>
import header from './components/header/header.vue'
const ERR_OK = 0
export default {
  name: 'app',
  components: {
    'v-header': header
  },
  date () {
    return {
      seller: {}
    }
  },
  created () {
    this.$http.get('/api/seller').then((response) => {
      response = response.body
      console.log(response)
      if (response.errno === ERR_OK) {
        this.seller = response.data
        console.log(this.seller)
      }
    })
  }
}
</script>

<style scoped lang="stylus">

  .title
    display: flex
    width: 100%
    height: 40px
    line-height: 40px
    .title-item
      flex: 1
      text-align: center
  .bottom
    position: fixed
    left: 0
    bottom:0
    width: 100%
    height: 46px
    background: rgba(7, 17, 27, 0.9)
    filter: blur(3px)
    z-index: 50
</style>

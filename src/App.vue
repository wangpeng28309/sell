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
    <router-view></router-view>
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
</style>

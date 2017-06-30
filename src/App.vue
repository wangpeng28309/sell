<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <P>
    <router-link to="/goods">商品</router-link>
    <router-link to="/ratings">评论</router-link>
    <router-link to="/seller">商家</router-link>
    </P>
    <router-view></router-view>
  </div>
</template>

<script>
import header from './components/header.vue'
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

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

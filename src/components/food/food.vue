<template>
  <transition name="move">
    <div v-show="showFlag" class="food">
      <div class="food-content">
        <div class="image-header">
          <img :src="food.image">
          <div class="back" @click="back()">
            <span class="icon-arrow_lift"></span>
          </div>
        </div>
        <div class="content">
          <h1 class="title">{{food.name}}</h1>
          <div class="detail">
            <span>月售{{food.sellCount}}份</span>
            <span>好评率{{food.rating}}%</span>
          </div>
          <div class="price">
            <span>${{food.price}}</span>
          </div>
        </div>
      </div>
      <div class="info" v-show="food.info">
        <h1 class="title">商品介绍</h1>
        <p class="detail">{{food.info}}</p>
      </div>
      <div class="ratings">
        <h1 class="title">商品评价</h1>
        <ratingselect :ratings="food.ratings" @select="selectEvent" @toggleContent="toggleContentEvent"></ratingselect>
        <div class="content">
          <ul class="rating-content">
            <li class="rating" v-for="item in food.ratings" v-show="needShow(item.rateType, item.text)">
              <span class="time">{{new Date(item.rateTime)}}</span>
              <span class="text">{{item.text}}</span>
              <img class="avatar" width="12" height="12" :src="item.avatar">
              <span class="username">{{item.username}}</span>
              <span :class="{'icon-thumb_up': item.rateType === 0, 'icon-thumb_down': item.rateType === 1}"></span>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
import ratingselect from '../ratingselect/ratingselect.vue'
export default {
  name: 'food',
  data () {
    return {
      showFlag: false,
      selectType: 2,
      onlyContent: false
    }
  },
  props: {
    food: {
      type: Object
    }
  },
  components: {
    ratingselect
  },
  computed: {
    starType () {
      return 'star-' + this.size
    }
  },
  methods: {
    show () {
      this.showFlag = true
    },
    back () {
      this.showFlag = false
    },
    needShow (type, text) {
      if (this.onlyContent && !text) {
        return false
      }
      if (this.selectType === 2) {
        return true
      } else {
        return type === this.selectType
      }
    },
    selectEvent (type) {
      this.selectType = type
      console.log(this.selectType)
    },
    toggleContentEvent () {
      this.onlyContent = !this.onlyContent
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
.food
  overflow: auto
  position: fixed
  top: 0
  left: 0
  bottom: 0
  z-index: 30
  width: 100%
  background: #fff
  &.move-enter-active, &.move-leave-active
    transition: all 0.2s linear
  &.move-enter, &.move-leave-active
    transform: translate3d(100%, 0, 0)
  .image-header
    position: relative
    width: 100%
    padding-top: 100%
    height: 0
    img
      position: absolute
      top: 0
      left: 0
      width: 100%
      height: 100%
    .back
      position: fixed
      top: 10px
      left: 5px
      color: #f3f5f7
</style>

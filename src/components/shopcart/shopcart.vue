<template>
<div class="shopcart">
  <div class="content">
    <div class="content-left">
      <div class="logo-wrapper">
        <div class="logo" :class="{'highlight': totalCount > 0}">
          <span class="icon-shopping_cart" :class="{'highlight': totalCount > 0}"></span>
        </div>
        <div class="number" v-show="totalCount > 0">{{totalCount}}</div>
      </div>
      <div class="price" :class="{'highlight': totalPrice > 0}">
        <div>¥{{totalPrice}}</div>
      </div>
      <div class="desc">
        <div>另需配送费{{seller.deliveryPrice}}元</div>
      </div>
    </div>
    <div class="content-right">
      <div class="pay" :class="{'highlight': totalPrice >= 20}">
        {{payDesc}}
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'shopcart',
  props: {
    seller: {
      type: Object
    },
    selectFoods: {
      type: Array,
      default () {
        return [
          {
            price: 10,
            count: 2
          }
        ]
      }
    }
  },
  computed: {
    totalPrice () {
      let total = 0
      this.selectFoods.forEach((food) => {
        total += food.price * food.count
      })
      return total
    },
    totalCount () {
      let count = 0
      this.selectFoods.forEach((food) => {
        count += food.count
      })
      return count
    },
    payDesc () {
      if (this.totalPrice === 0) {
        return `¥${this.seller.minPrice}元起送`
      } else if (this.totalPrice < this.seller.minPrice) {
        let diff = this.seller.minPrice - this.totalPrice
        return `还差¥${diff}元起送`
      } else {
        return '去结算'
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
.shopcart
  position: fixed
  left: 0
  bottom:0
  width: 100%
  height: 46px
  z-index: 50
  .content
    display: flex
    background: #141d27
    font-size: 0
    .content-left
      flex: 1
      .logo-wrapper
        display: inline-block
        position: relative
        top: -10px
        margin: 0 12px
        padding: 6px
        width: 56px
        height: 56px
        box-sizing: border-box
        vertical-align: top
        border-radius: 50%
        background: #141d27
        .logo
          width:100%
          height:100%
          border-radius: 50%
          text-align: center
          background: #2b343c
          &.highlight
            background: rgb(0, 160, 220)
          .icon-shopping_cart
            line-height: 44px
            font-size: 24px
            color: #80858a
            &.highlight
              color: #fff
        .number
            position: absolute
            top: 0
            right: 0
            width: 24px
            height: 16px
            line-height: 16px
            text-align: center
            border-radius: 16px
            font-size: 9px
            font-weight: 700
            color: #fff
            background: rgb(240, 20, 20)
            box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.4)
      .price
        display: inline-block
        vertical-align: top
        margin-top: 12px
        line-height: 24px
        padding-right: 12px
        box-sizing: border-box
        border-right: 1px solid rgba(255, 255, 255, 0.1)
        font-size: 16px
        font-weight: 700
        color: #1f2f3f
        &.highlight
          color: white
      .desc
        display: inline-block
        vertical-align: top
        margin: 12px 0 0 12px
        line-height: 24px
        font-size: 10px
        color: white
    .content-right
      flex: 0 0 105px
      width: 105px
      .pay
        height: 48px
        line-height: 48px
        text-align: center
        font-size: 12px
        font-weight: 700
        color: #1f2f3f
        &.highlight
          background: rgb(0, 160, 220)
          color: white
</style>

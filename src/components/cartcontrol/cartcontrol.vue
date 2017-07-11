<template>
  <div class="cartcontrol">
    <span class="icon-remove_circle_outline" @click.stop.prevent="remove($event)" v-show="food.count"></span>
    <span class="number" v-show="food.count">{{food.count}}</span>
    <span class="icon-add_circle" @click.stop.prevent="add($event)"></span>
  </div>
</template>

<script>
import Vue from 'vue'
export default {
  name: 'cartcontrol',
  props: {
    food: {
      type: Object
    }
  },
  methods: {
    add (event) {
      if (!event._constructed) {
        return
      } else {
        if (!this.food.count) {
          Vue.set(this.food, 'count', 1)
        } else {
          this.food.count ++
        }
      }
    },
    remove (event) {
      if (!event._constructed) {
        return
      } else {
        if (!this.food.count) {
          return
        } else {
          this.food.count --
        }
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">

</style>

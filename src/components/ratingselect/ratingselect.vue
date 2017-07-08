<template>
  <div class="select-rating">
    <div class="select-type">
      <span class="all" @click="select(2, $event)">全部{{ratings.length}}</span>
      <span class="positive" @click="select(0, $event)">推荐{{positiveRatings.length}}</span>
      <span class="negative" @click="select(1, $event)">吐槽{{negativeRatings.length}}</span>
    </div>
    <div class="select-content" @click="toggleContent()">
      <span class="icon-check_circle"></span>
      <span class="text">只看有内容的评价</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ratingselect',
  props: {
    ratings: {
      type: Array
    }
  },
  computed: {
    positiveRatings () {
      return this.ratings.filter((rating) => {
        return rating.rateType === 0
      })
    },
    negativeRatings () {
      return this.ratings.filter((rating) => {
        return rating.rateType === 1
      })
    }
  },
  methods: {
    select (type, event) {
      this.$emit('select', type)
      console.log(type)
    },
    toggleContent (event) {
      this.$emit('toggleContent')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">

</style>

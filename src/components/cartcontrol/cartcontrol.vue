<template>
  <div class="cartcontrol">
    <span class="icon-remove_circle_outline" @click.stop.prevent="remove()"></span>
    <span class="number">{{number}}</span>
    <span class="icon-add_circle" @click.stop.prevent="add()"></span>
  </div>
</template>

<script>
export default {
  name: 'cartcontrol',
  data () {
    return {
      number: 0
    }
  },
  methods: {
    add () {
      this.number ++
    },
    remove () {
      this.number --
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">

</style>

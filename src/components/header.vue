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

    </div>  
    <div class="bulletin-wrapper"></div>
  </div>
</template>

<script>
export default {
  name: 'header',
  props: {
    seller: {
      type: Object
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>

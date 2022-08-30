<template>
    <p class="circleTop" :style="{fontSize:homeFont}">{{menuname}}</p>
</template>
<script>
export default {
  props: {
    menuname: String
  },
  data () {
    return {
      homeFont: '3vw'
    }
  }
}
</script>

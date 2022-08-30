<template>
     <header v-show="header">
                <ul>
                    <li id="header-cube"><a href="#" @click="home" class="menuColor">
                        <div class="one">home</div>
                        <div class="two">home</div>
                        <div class="three">home</div>
                        <div class="four">home</div>
                        <div class="five">home</div>
                        <div class="six">home</div>
                    </a></li>
                    <li><a href="#" @click="section" class="menuColor">{{navName[0]}}</a></li>
                    <li><a href="#" @click="section" class="menuColor">{{navName[1]}}</a></li>
                    <li><a href="#" @click="section" class="menuColor">{{navName[2]}}</a></li>
                    <li><a href="#" @click="section" class="menuColor">{{navName[3]}}</a></li>
                    <li><a href="#" @click="section" class="menuColor">{{navName[4]}}</a></li>
                </ul>
            </header>
</template>
<script>
export default {
  props: {
    header: Boolean,
    navName: Array
  },
  methods: {
    home (e) {
      this.$emit('home', e)
    },
    section (e) {
      this.$emit('section', e)
    }
  }
}
</script>

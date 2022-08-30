<template>
  <transition name="scale">
    <div id="full" v-show="sub" @wheel.prevent="subWheel">
                <!-- <div v-for="(item,index) in circleStyle" :key="item"class="full">{{index}}</div> -->
                <div class="full" id="outer">

                    <ul id="project" @mousedown="mDown" @mouseup="mUp" @mousemove="mMove">
                        <li id="project1" class="moveI">
                            <h2>{{navName[0]}}-1</h2>
                            <div>
                                <div class="project-text">

                                </div>
                                <div class="project-img">
                                    <!-- <img src="img/music.png" alt=""> -->
                                </div>
                            </div>
                        </li>
                        <li class="moveI">
                            <h2>{{navName[0]}}-2</h2>
                            <div>
                            </div>
                        </li>
                        <li class="moveI">
                            <h2>{{navName[0]}}-3</h2>
                            <div>
                            </div>
                        </li>
                        <li class="moveI">
                            <h2>{{navName[0]}}-4</h2>
                            <div>
                            </div>
                        </li>
                        <li class="moveI">
                            <h2>{{navName[0]}}-5</h2>
                            <div>
                            </div>
                        </li>

                    </ul>

                </div>
                <div class="full">
                    <div>
                        <h2>{{navName[1]}}</h2>
                        <div></div>
                    </div>
                </div>
                <div class="full">
                    <div>
                        <h2>{{navName[2]}}</h2>
                        <div></div>
                    </div>
                </div>
                <div class="full">
                    <div>
                        <h2>{{navName[3]}}</h2>
                        <div></div>
                    </div>
                </div>
                <div class="full">
                    <div>
                        <h2>{{navName[4]}}</h2>
                        <div></div>
                    </div>
                </div>
            </div>
  </transition>

</template>
<script>
export default {
  props: {
    navName: Array,
    sub: Boolean
  },
  data () {
    return {
      press: false,
      startx: null,
      up: null,
      projectI: 0,
      moveI: 0
    }
  },
  methods: {
    subWheel (e) {
      this.$emit('subWheel', e)
    },
    mDown (e) {
      const innerUl = document.querySelector('#project')
      this.press = true
      this.startx = e.offsetX - innerUl.offsetLeft
      innerUl.style.transition = 'none'
    },
    mUp () {
      this.press = false
      const innerUl = document.querySelector('#project')
      innerUl.style.transition = '0.5s'
      if (this.up < 0) {
        this.projectI++
        this.moveI++
        innerUl.style.marginLeft = -100 * this.projectI + 'vw'
        this.up = null
      } else if (this.up > 0) {
        this.projectI--
        this.moveI--
        innerUl.style.marginLeft = -100 * this.projectI + 'vw'
        this.up = null
      }
    },
    mMove (e) {
      const innerUl = document.querySelector('#project')
      const ch = innerUl.clientWidth - document.getElementById('project1').clientWidth
      if (!this.press) return
      e.preventDefault()
      innerUl.style.marginLeft = e.offsetX - this.startx + 'px'
      if (parseInt(innerUl.style.marginLeft) > 0) {
        innerUl.style.marginLeft = '0px'
      } else if (parseInt(innerUl.style.marginLeft) < -ch) {
        innerUl.style.marginLeft = -ch + 'px'
      }
      if (parseInt(innerUl.style.marginLeft) <= 0 || parseInt(innerUl.style.marginLeft) > -ch) {
        this.up = document.querySelectorAll('.moveI')[this.moveI].offsetLeft
      }
    }
  }
}
</script>

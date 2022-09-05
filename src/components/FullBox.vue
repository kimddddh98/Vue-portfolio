<template>
    <div id="full" v-show="sub" @wheel.prevent="subWheel">
      <div class="full" id="outer">
        <ul id="project" @mousedown="mDown" @mouseup="mUp" @mousemove="mMove">
          <li id="project1" class="moveI">
            <h2>{{navName[0]}}-1</h2>
            <div>
                <div class="project-text">
                </div>
                <div class="project-img">
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
              <div id="about">
                <div id="aboutTop">사진</div>
                <div id="aboutBot">
                  <div>asd</div>
                  <p>김동현</p>
                  <p>1998.12.10</p>
                  <p>경기도 안산시 거주</p>
                  <p>amawang11@gmail.com</p>
                  <p>2022.03 ~ 2022.09 라인컴퓨터아트학원 UI/UX 디자인 & 웹펴블리셔 과정</p>
                  <p>웹디자인기능사(09.08 합격자발표)</p>
                </div>
              </div>
          </div>
      </div>
      <div class="full">
          <div>
              <h2>{{navName[2]}}</h2>
              <div id="skill">
                <div>
                  <div><img :src="img[0]" alt="html"></div>
                  <div><img :src="img[1]" alt="html"></div>
                  <div><img :src="img[2]" alt="html"></div>
                </div>
                <div>
                  <div><img :src="img[3]" alt="html"></div>
                  <div><img :src="img[4]" alt="html"></div>
                  <div><img :src="img[5]" alt="html"></div>

                </div>
              </div>
          </div>
      </div>
      <div class="full">
          <div>
              <h2>{{navName[3]}}</h2>
              <div id="contact">
                <div>
                  <div class="front">H.P</div>
                  <div class="back">010-4252-3496</div>
                </div>
                <div>
                  <div class="front">E-mail</div>
                  <div class="back">amawang11@gmail.com</div>
                </div>
                <div>
                  <div class="front">a</div>
                  <div class="back">a</div>
                </div>
              </div>
          </div>
      </div>
      <div class="full">
          <div>
              <h2>{{navName[4]}}</h2>
              <div></div>
          </div>
      </div>
    </div>

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
      moveI: 0,
      img: [
        require('@/assets/html.png'),
        require('@/assets/css.png'),
        require('@/assets/js.png'),
        require('@/assets/jquery.png'),
        require('@/assets/vue.png'),
        require('@/assets/sass.png')
      ]
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
      innerUl.style.cursor = 'grabbing'
    },
    mUp () {
      this.press = false
      const innerUl = document.querySelector('#project')
      innerUl.style.cursor = 'auto'
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

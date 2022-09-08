<template>
  <div>
    <transition name="header">
      <FullHeaderVue :navName="navName" :header="header" @home="home" @section="section"></FullHeaderVue>
    </transition>
    <transition name="scale">
      <div id="container" v-show="main" @wheel="mainWheel">
        <div id="main-text">
          <div>Kim<br>Dong-Hyeon</div>
          <div>Front-end<br>Developer</div>
        </div>
        <div id="menu">
          <div id="circle">
            <div class="cube">
              <div v-for="cubeItem in cube" :key="cubeItem.cubeTitle" :class="cubeItem.cubeClass">
                <p>{{ cubeItem.cubeTitle }}</p>
              </div>
            </div>
          </div>
          <transition name="fade">
            <div @click="subPage" class="circleItem" :style="circleStyle[0]" v-if="transform">
              <MenuNameVue :menuname="navName[0]"></MenuNameVue>

            </div>
          </transition>
          <transition name="fade">
            <div @click="subPage" class="circleItem" :style="circleStyle[1]" v-if="transform">
              <MenuNameVue :menuname="navName[1]"></MenuNameVue>
            </div>
          </transition>

          <transition name="fade">
            <div @click="subPage" class="circleItem" :style="circleStyle[2]" v-if="transform">
              <MenuNameVue :menuname="navName[2]"></MenuNameVue>

            </div>
          </transition>
          <transition name="fade">
            <div @click="subPage" class="circleItem" :style="circleStyle[3]" v-if="transform">
              <MenuNameVue :menuname="navName[3]"></MenuNameVue>

            </div>
          </transition>

          <transition name="fade">
            <div @click="subPage" class="circleItem" :style="circleStyle[4]" v-if="transform">
              <MenuNameVue :menuname="navName[4]"></MenuNameVue>
            </div>
          </transition>
        </div>
      </div>
    </transition>

    <transition name="scale">
      <FullBox :sub="sub" :navName="navName" @subWheel="subWheel" :circleStyle="circleStyle"></FullBox>
    </transition>
  </div>
</template>
<script>
import FullHeaderVue from './components/FullHeader.vue'
import MenuNameVue from './components/MenuName.vue'
import FullBox from './components/FullBox.vue'
export default {
  mounted: function () {
    setTimeout(() => {
      this.transform = true
    }, 2500)
  },
  components: {
    MenuNameVue, FullBox, FullHeaderVue
  },
  data () {
    return {
      main: true,
      circleStyle: [
        { transform: 'rotateY(0deg) translateZ(30vw) translateY(0vw)', backgroundImage: 'linear-gradient(-225deg, #7DE2FC 0%, #B9B6E5 100%)' },
        { transform: 'rotateY(70deg) translateZ(30vw) translateY(10vw)', backgroundImage: 'linear-gradient(120deg,#8ec5fc 0%,#e0c3fc 100%)' },
        { transform: 'rotateY(140deg) translateZ(30vw) translateY(20vw)', backgroundImage: 'linear-gradient(to top, #9795f0 0%, #fbc8d4 100%)' },
        { transform: 'rotateY(210deg) translateZ(30vw) translateY(30vw)', backgroundImage: 'linear-gradient(-225deg, #A8BFFF 0%, #884D80 100%)' },
        { transform: 'rotateY(280deg) translateZ(30vw) translateY(40vw)', backgroundImage: ' linear-gradient(to top, #505285 0%, #585e92 12%, #65689f 25%, #7474b0 37%, #7e7ebb 50%, #8389c7 62%, #9795d4 75%, #a2a1dc 87%, #b5aee4 100%)' }
      ],
      cube: [
        { cubeTitle: 'CSS', cubeClass: 'one' },
        { cubeTitle: 'HTML', cubeClass: 'two' },
        { cubeTitle: 'Javascript', cubeClass: 'three' },
        { cubeTitle: 'CSS', cubeClass: 'four' },
        { cubeTitle: 'Vue', cubeClass: 'five' },
        { cubeTitle: 'Ajax', cubeClass: 'six' }
      ],
      transform: false,
      navName: ['Project', 'About Me', 'Skill', 'Contact', 'More'],
      click: 0,
      sub: false,
      header: false,
      headerColor: '#fefefe',
      headerFocus: 'rgb(138, 170, 229)',
      timer: false
    }
  },
  methods: {
    subWheel (e) {
      if (this.timer === false) {
        const fullbox = document.querySelectorAll('.full')
        const full = document.getElementById('full')
        const headerMenu = document.querySelectorAll('.menuColor')
        this.timer = true
        this.timer = setTimeout(() => {
          this.timer = false
        }, 600)
        if (e.wheelDelta <= 0) {
          if (this.click !== fullbox.length - 1 && this.click < fullbox.length - 1) {
            for (let i = 0; i < fullbox.length; i++) {
              fullbox[i].style.width = 90 + 'vw'
              fullbox[i].style.height = 85 + 'vh'
            }
            if (this.click < headerMenu.length - 2) {
              for (let h = 0; h < headerMenu.length; h++) {
                headerMenu[h].style.color = this.headerColor
                headerMenu[h].parentNode.style.backgroundColor = 'transparent'
              }
              headerMenu[this.click + 2].style.color = this.headerFocus
              headerMenu[this.click + 2].parentNode.style.backgroundColor = '#fefefe'
            }
            full.style.left = -100 * (this.click + 1) + 'vw'
            setTimeout(() => {
              for (let i = 0; i < fullbox.length; i++) {
                fullbox[i].style.width = 100 + 'vw'
                fullbox[i].style.height = 100 + 'vh'
              }
              this.click + 1 >= fullbox.length - 1 ? this.click = fullbox.length - 1 : this.click++
            }, 600)
          }
        } else {
          if (this.click !== 0 && this.click > 0) {
            for (let i = 0; i < fullbox.length; i++) {
              fullbox[i].style.width = 90 + 'vw'
              fullbox[i].style.height = 85 + 'vh'
            }
            for (let h = 0; h < headerMenu.length; h++) {
              headerMenu[h].style.color = this.headerColor
              headerMenu[h].parentNode.style.backgroundColor = 'transparent'
            }
            headerMenu[this.click].style.color = this.headerFocus
            headerMenu[this.click].parentNode.style.backgroundColor = '#fefefe'

            full.style.left = -100 * (this.click - 1) + 'vw'
            setTimeout(() => {
              for (let i = 0; i < fullbox.length; i++) {
                fullbox[i].style.width = 100 + 'vw'
                fullbox[i].style.height = 100 + 'vh'
              }
              this.click <= 0 ? this.click = 0 : this.click--
            }, 600)
          }
        }
      }
    },
    subPage: function (e) {
      const headerMenu = document.querySelectorAll('.menuColor')
      const full = document.getElementById('full')
      this.main = false
      this.transform = false
      setTimeout(() => {
        this.header = true
        this.sub = true
        // document.getElementsByTagName('body').style.backgroundColor = this.headerFocus
        document.getElementById('project').style.width = this.circleStyle.length * 100 + '%'
        full.style.width = this.circleStyle.length * 100 + 'vw'
        for (let i = 0; i < document.querySelectorAll('.circleItem').length; i++) {
          if (e.target === document.querySelectorAll('.circleItem')[i]) {
            this.click = i
          }
        }
        full.style.left = -100 * this.click + 'vw'
        headerMenu[this.click + 1].style.color = this.headerFocus
        headerMenu[this.click + 1].parentNode.style.backgroundColor = '#fefefe'
      }, 500)
    },
    mainWheel: function (e) {
      const found = /-\d+|\d+/g
      const circleItem = document.querySelectorAll('.circleItem')
      const circleArr = []
      if (e.wheelDelta <= 0) {
        if (circleItem[0].style.transform !== 'rotateY(-280deg) translateZ(30vw) translateY(-40vw)') {
          for (let i = 0; i < circleItem.length; i++) {
            circleArr.push(circleItem[i].style.transform.match(found))
            circleItem[i].style.transform =
                              `rotateY(${parseInt(circleArr[i][0]) - 35}deg) translateZ(30vw) translateY(${parseInt(circleArr[i][2]) - 5}vw)`
          }
        }
      } else {
        if (circleItem[0].style.transform !== 'rotateY(0deg) translateZ(30vw) translateY(0vw)') {
          for (let i = 0; i < circleItem.length; i++) {
            circleArr.push(circleItem[i].style.transform.match(found))
            circleItem[i].style.transform =
                              `rotateY(${parseInt(circleArr[i][0]) + 35}deg) translateZ(30vw) translateY(${parseInt(circleArr[i][2]) + 5}vw)`
          }
        }
      }
    },
    home (e) {
      e.preventDefault()
      this.header = false
      this.sub = false
      // this.main = true
      this.click = 0
      setTimeout(() => {
        this.main = true
      }, 1000)
      setTimeout(() => {
        this.transform = true
      }, 3500)
      const headerMenu = document.querySelectorAll('.menuColor')
      for (let h = 0; h < headerMenu.length; h++) {
        headerMenu[h].style.color = this.headerColor
        headerMenu[h].parentNode.style.backgroundColor = 'transparent'
      }
    },
    section (e) {
      e.preventDefault()
      const full = document.getElementById('full')
      const fullbox = document.querySelectorAll('.full')
      const headerMenu = document.querySelectorAll('.menuColor')
      for (let h = 0; h < headerMenu.length; h++) {
        headerMenu[h].style.color = this.headerColor
        headerMenu[h].parentNode.style.backgroundColor = 'transparent'
        e.target.style.color = this.headerFocus
        e.target.parentNode.style.backgroundColor = '#fefefe'
        if (headerMenu[h].style.color === 'rgb(138, 170, 229)') { this.click = h - 1 }
      }
      for (let i = 0; i < fullbox.length; i++) {
        fullbox[i].style.width = 90 + 'vw'
        fullbox[i].style.height = 85 + 'vh'
      }
      full.style.left = -100 * this.click + 'vw'
      setTimeout(() => {
        for (let i = 0; i < fullbox.length; i++) {
          fullbox[i].style.width = 100 + 'vw'
          fullbox[i].style.height = 100 + 'vh'
        }
      }, 600)
    }
  }
}
</script>
  <style lang="scss">
  @charset "utf-8";
  @import url('https://fonts.googleapis.com/css2?family=Cormorant+SC&family=Fugaz+One&display=swap');
  @import url('https://fonts.googleapis.com/css2?family=Nosifer&display=swap');
  @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+KR&display=swap');
  *{
      margin: 0;
      padding: 0;
      box-sizing: border-box;
  }

  a{
      color: #333;
      text-decoration: none;
  }
  ul,li,ol{
      list-style: none;
  }

  // $bg: rgb(138, 170, 229);
  $bg:#8AAAE5;
  $color: #fefefe;
  $grColor:radial-gradient(circle, rgba(237,242,246,1) 8%, rgba(138,170,229,1) 78%);
  $boxFont:  'Cormorant SC', serif;
  $koFont: 'Noto Sans KR', sans-serif;
  // $boxFont: 'Fugaz One', cursive;
  $mainFont: 'Nosifer', cursive;
  @mixin flexCenter {
      display: flex;
      justify-content: center;
      align-items: center;
  }
  @keyframes spin {

      from {
          transform: rotateY(0) rotateX(0);
      }

      to {
          transform: rotateY(-360deg) rotateX(360deg);
      }
  }
  html,
  body {
      width: 100%;
      height: 100%;
      overflow: hidden;
      background: $grColor
  }
  header {
      width: 100vw;
      padding: 20px 0;
      position: fixed;
      z-index: 9;
      #header-cube{
          width: 3vw;
          transform:skewX(0deg);
          position: relative;
          border: none;
          &>a{
              width: 3vw;
              height: 3vw;
              position: absolute;
              top: 0;
              transform:skewX(0deg);
              animation: spin 5s infinite linear;
              transform-style: preserve-3d;
              font-family: $boxFont;
          }
          a>div {
              width: 3vw;
              height: 3vw;
              position: absolute;
              border: 1px solid $bg;
              background-color: $color;
              opacity: .8;
              display: flex;
              justify-content: center;
              align-items: center;
              color: $bg;
          }
          .one {
              transform: rotateY(90deg) translateZ(1.5vw);
          }
          .two {
              transform: translateZ(1.5vw);
          }

          .three {
              transform: rotateY(-90deg) translateZ(1.5vw);
          }

          .four {
              transform: rotateX(90deg)translateZ(1.5vw);
          }

          .five {
              transform: rotateX(-90deg) translateZ(1.5vw);
          }

          .six {
              transform: rotateX(180deg) translateZ(1.5vw);
          }

      }
      ul {
          display: flex;
          justify-content: space-around;
          font-size: 1vw;
          li{
              width: 11vw;
              text-align: center;
              padding: 0.4vw 0;
              border: 2px solid $color;
              transform: skewX(-45deg);
          }
          a {
              transform: skewX(45deg);
              display: block;
              width: 100%;
              height: 100%;
              color:$color;
          }
      }
  }

  #app {
      height: 100%;
  }

  #container {
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      perspective: 4000px;

      #main-text {
          position: absolute;
          width: 100vw;
          height: 100vh;
          top: 0;
          left: 0;
          color: $color;
          display: flex;
          justify-content: space-between;
          font-family: $mainFont;
          font-size: 2vw;

          &>div:nth-of-type(2) {
              align-self: flex-end;
              text-align: center;
          }
      }
  }

  #menu {
      width: 33vw;
      height: 33vw;
      position: relative;
      transform-style: preserve-3d;
      #circle {
          width: 100%;
          height: 100%;
          position: absolute;
          display: flex;
          justify-content: center;
          align-items: center;

          .cube {
              width: 16.5vw;
              height: 16.5vw;
              position: relative;
              top: 0;
              animation: spin 5s infinite linear;
              animation-delay: 2.5s;
              transform-style: preserve-3d;
              font-family: $boxFont;

              &>div {
                  width: 16.5vw;
                  height: 16.5vw;
                  position: absolute;
                  border: 2px solid $bg;
                  background-color: $color;
                  opacity: .8;
                  display: flex;
                  justify-content: center;
                  align-items: center;
                  font-size: 2vw;
                  color: $bg;
              }
              @keyframes scale1 {
                  0% {
                      transform: translateX(16.5vw) translateZ(8.25vw);
                  }
                  100% {
                      transform: rotateY(90deg) translateZ(8.25vw);
                  }
              }
              @keyframes scale3 {
                  0% {
                      transform: translateX(-16.5vw) translateZ(8.25vw);
                  }
                  100% {
                      transform: rotateY(-90deg) translateZ(8.25vw);
                  }
              }
              @keyframes scale4 {
                  0% {
                  transform: translateY(-16.5vw) translateZ(8.25vw);
                  }
                  100% {
                  transform: rotateX(90deg)translateZ(8.25vw);
                  }
              }
              @keyframes scale5 {
                  0% {
                      transform: translateY(16.5vw) translateZ(8.25vw);
                  }
                  100% {
                  transform: rotateX(-90deg) translateZ(8.25vw);
                  }
              }
              @keyframes scale6 {
                  0% {
                      transform: translateY(33vw) translateZ(8.25vw);

                  }
                  100% {
                  transform: rotateX(180deg) translateZ(8.25vw);
                  }
              }
              .one {
                  transform: translateX(16.5vw) translateZ(8.25vw);
                  animation: scale1 1.5s both;
                  animation-delay: 0.5s;
              }

              .two {
                  transform: translateZ(8.25vw);
              }

              .three {
                  transform: translateX(-16.5vw) translateZ(8.25vw);
                  animation: scale3 1.5s both;
                  animation-delay: 0.5s;
              }

              .four {
                  transform: translateY(-16.5vw) translateZ(8.25vw);
                  animation: scale4 1.5s both;
                  animation-delay: 0.5s;
              }

              .five {
                  transform: translateY(16.5vw) translateZ(8.25vw);
                  animation: scale5 1.5s both;
                  animation-delay: 0.5s;
              }

              .six {
                  transform: translateY(33vw) translateZ(8.25vw);
                  animation: scale6 1.5s both;
                  animation-delay: 0.5s;
              }
          }
      }
      .circleItem {
          cursor: pointer;
          position: absolute;
          top: 0;
          left: 0;
          width: 30vw;
          height: 30vw;
          opacity: 0.9;
          transition: 1s;
          display: flex;
          align-items: center;
          justify-content: center;
          p{
              font-size: 3vw;
              color: $color;
              font-family: $boxFont;
              pointer-events: none;
          }
          img {
              width: 100%;
              height: 100%;
          }
      }

  }
  .scale-enter-active,
  .scale-leave-active {
    animation: fullFade 1s;

  }
  .scale-enter,
  .scale-leave-to {
    animation: fullFade 1s reverse;

  }
  .fade-enter-active,
  .fade-leave-active {
      animation: mainFadeIn 1s;
  }
  .fade-enter,
  .fade-leave-to {
      opacity: 0;
  }
  .header-enter-active,
  .header-leave-active {
      animation: headerFade 1s;
  }
  .header-enter,
  .header-leave-to {
    animation: headerFade 0.5s reverse;
  }
  @keyframes fullFade{
    0%{
      transform: scale(0.5);
      opacity: 0;
    }
    100%{
      transform: scale(1);
      opacity: 1;
    }
  }
  @keyframes headerFade{
    0%{
      transform: translateY(-50px);
      opacity: 0;
    }
    100%{
      transform: translateY(0px);
      opacity: 1;
    }
  }
  @keyframes mainFadeIn{
      0%{
          opacity: 0;
      }
      100%{
          opacity: 0.9;
      }
  }
  @mixin subBox {
      height: 92%;
      align-self: flex-end;
      flex-direction: column;
      display: flex;
      align-items: center;
      color: $color;
      font-family: $boxFont;
      &>h2{
          text-align: center;
          font-size: 2vw;
          padding: 20px;
      }
      &>div{
          width: 90%;
          height: 85%;
          border: 2px solid $color;
      }
      @content;
  }
  @mixin arrow{
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  z-index: 3;
  cursor: pointer;
    img{
      width:3vw
    }
    @content;
  }
  #wheel-left{
  @include arrow;
  left: 0.5vw;
  // display: none

}
#wheel-right{
  @include arrow;
  right:0.5vw;
  transform: rotate(180deg);
}
  #full {
      width: 500vw;
      height: 100vh;
      display: flex;
      align-items: center;
      justify-content: space-around;
      position: relative;
      transition: all 0.6s;
      background-color: #a8c0ee;
      &>.full {
          width: 100vw;
          height: 100vh;
          transition: all 0.4s;
          overflow: hidden;
          position: relative;
          &:not(:first-of-type){
              display: flex;
          }
          &>.full-sub{
              width: 100%;
              @include subBox
          }
      }

      #project {
          width: 500%;
          height: 100%;
          display: flex;
          align-items: center;
          cursor: grab;
          li {
              width: 20%;
              pointer-events: none;

              @include subBox;
              &>div{
                  display:flex;
                  &>div{
                  width: 50%;
                  overflow: hidden;
                  position: relative;
                  img{
                      width: 100%;
                      position: absolute;
                      top: 0;
                      transition: 5s linear;
                      pointer-events: all;
                  }
                }
             }
          }
      }
  }
  .project-text{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-around;
    font-family: $koFont;
    font-size: 1.2vw;

    .text-box{
      display: flex;
      align-items: center;
      width: 80%;
      height: 70%;
      line-height: 2vw;

    }
    .button-box{
      width: 50%;
      height: 10%;
      display: flex;
      justify-content: space-between;
      pointer-events:all;
      &>a{
        width: 49%;
        height: 100%;
        background-color: $color;
        border: 1px solid $bg;
        color: $bg;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 1.5vw;
        transition: 0.3s ease-in;
        &:hover{
          // background: ;
          background-color: transparent;
          color: $color;
          border:1px solid $color
        }
      }
    }
  }
#about{
  display: flex;
  justify-content: space-around;
  align-items: center;
  font-family: $koFont;
  font-size: 23px;
  &Top{
    width: 20%;
    height: 50%;

    border: 2px solid $color;
  }
  &Bot{
    width: 60%;
    height: 80%;

    border-left: 2px solid $color;
    // background-color: aquamarine;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    &>div{
      width: 90%;
      height: 20%;
      align-self: flex-end;
      // background-color:blue;
    }
    &>p{
      width: 90%;
      align-self: flex-end;
    }
  }
}
#skill{
  display: flex;
  flex-direction: column;
  &>div{
    width:100%;
    height: 50%;
    display: flex;
    &:first-of-type{
      border-bottom: 2px solid $color;
    }
    &>div{
      width: 25%;
      height: 100%;
      // border:1px solid #333;
      display: flex;
      justify-content: center;
      align-items: center;
      // background-color:#3f568b ;
      &:nth-of-type(2){
        border-left: 2px solid $color;
        border-right: 2px solid $color;
      }
      &:nth-of-type(3){
        border-right: 2px solid $color;
      }
      &>img{
        width: 60%;
      }
    }
  }
}
#contact{
  display: flex;
  justify-content: space-around;
  align-items: center;
  &>div{
    width: 28%;
    height: 55%;
    position: relative;
    &:hover .front{
      transform: rotateY(180deg);
    }
    &:hover .back{
      transform: rotateY(0deg);
    }
    &>div{
      width: 100%;
      height: 100%;
      color: $bg;
      background-color: $color;
      border: 1px solid $bg;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      backface-visibility: hidden;
      transition: 1s;
      cursor: pointer;
    }
    .front{
        transform: rotateY(0);
        position: absolute;
        font-size: 2vw;

        &>p{
          padding: 10px 0;

        }
        &>div{
          width: 20%;
          height: 30%;
          img{
            width: 100%;
          }
        }
      }
      .back{
        transform: rotateY(-180deg);
        font-family: $koFont;
        font-size: 1.5vw;

        &>input{
          border: none;
          color: $bg;
          background-color: transparent;
          outline: none;
          text-align: center;
          font-size: 1.5vw;
          font-family: $koFont;
        }
      }
  }
}
#more{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  &>h2{
    font-size: 3vw;
    width: 70%;
    height: 10%;
    text-align: center;
  }
  &>div{
    text-align: center;
    width: 70%;
    height: 40%;
    font-size: 1.7vw;
    font-family: $koFont;
  }
}

</style>

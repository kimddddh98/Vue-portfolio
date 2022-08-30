<template>
  <div>
    <FullHeaderVue :navName="navName" :header="header" @home="home" @section="section"></FullHeaderVue>
    <transition name="scale">
  <div id="container" v-show="main" @wheel="mainWheel">
      <div id="main-text">
          <div>Kim<br>Dong-Hyeon</div>
          <div>Front-end<br>Developer vue</div>
      </div>
      <div id="menu">
          <div id="circle">
              <div class="cube">
                  <div v-for="cubeItem in cube" :key="cubeItem.cubeTitle" :class="cubeItem.cubeClass">
                      <p>{{cubeItem.cubeTitle}}</p>
                  </div>
              </div>
          </div>
          <!-- <div v-for="(item,index) in circleStyle" @click="subPage" @mouseover="circleOver" @mouseout="circleOut" class="circleItem" :style="item" :key="item" >{{index}} </div> -->
          <!-- <div v-for="(item,index) in circleStyle" @click="subPage" @mouseover="circleOver" @mouseout="circleOut" class="circleItem" :style="item" :key="item" >{{index}} </div> -->
          <transition name="fade">
              <div @click="subPage" class="circleItem"
                  :style="circleStyle[0]" v-if="transform">
                  <MenuNameVue :menuname="navName[0]"></MenuNameVue>

              </div>
          </transition>
          <transition name="fade">
              <div @click="subPage" class="circleItem"
                  :style="circleStyle[1]" v-if="transform">
                  <MenuNameVue :menuname="navName[1]"></MenuNameVue>
              </div>
          </transition>

          <transition name="fade">
              <div @click="subPage" class="circleItem"
                  :style="circleStyle[2]" v-if="transform">
                  <MenuNameVue :menuname="navName[2]"></MenuNameVue>

              </div>
          </transition>
          <transition name="fade">
              <div @click="subPage" class="circleItem"
                  :style="circleStyle[3]" v-if="transform">
                  <MenuNameVue :menuname="navName[3]"></MenuNameVue>

              </div>
          </transition>

          <transition name="fade">
              <div @click="subPage" class="circleItem"
                  :style="circleStyle[4]" v-if="transform">
                  <MenuNameVue :menuname="navName[4]"></MenuNameVue>
              </div>
          </transition>
      </div>
  </div>
  </transition>
    <FullBox :sub="sub" :navName="navName" @subWheel="subWheel"></FullBox>
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
        { transform: 'rotateY(70deg) translateZ(30vw) translateY(10vw)', backgroundImage: ' linear-gradient(120deg,#8ec5fc 0%,#e0c3fc 100%) ' },
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
      headerColor: '#fefefe'
    }
  },
  methods: {
    subWheel (e) {
      if (!this.timer) {
        this.timer = setTimeout(() => {
          this.timer = null
          const fullbox = document.querySelectorAll('.full')
          const full = document.getElementById('full')
          const headerMenu = document.querySelectorAll('.menuColor')
          if (e.wheelDelta <= 0) {
            if (this.click !== fullbox.length - 1 && this.click < fullbox.length - 1) {
              for (let i = 0; i < fullbox.length; i++) {
                fullbox[i].style.width = 90 + 'vw'
                fullbox[i].style.height = 85 + 'vh'
              }
              // this.click = fullbox.length
              if (this.click < headerMenu.length - 2) {
                for (let h = 0; h < headerMenu.length; h++) {
                  headerMenu[h].style.color = this.headerColor
                  headerMenu[h].parentNode.style.backgroundColor = 'transparent'
                }
                headerMenu[this.click + 2].style.color = '#8AAAE5'
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
              headerMenu[this.click].style.color = '#8AAAE5'
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
        }, 200)
      }
    },
    subPage: function (e) {
      const headerMenu = document.querySelectorAll('.menuColor')
      const full = document.getElementById('full')
      full.style.width = this.circleStyle.length * 100 + 'vw'
      this.main = false
      this.transform = false
      setTimeout(() => {
        this.header = true
        this.sub = true
        document.getElementById('project').style.width = this.circleStyle.length * 100 + '%'
      }, 500)
      for (let i = 0; i < document.querySelectorAll('.circleItem').length; i++) {
        if (e.target === document.querySelectorAll('.circleItem')[i]) {
          setTimeout(() => {
            full.style.left = -100 * i + 'vw'
            headerMenu[i + 1].style.color = '#8AAAE5'
            headerMenu[i + 1].parentNode.style.backgroundColor = '#fefefe'
          }, 100)
          this.click = i
        }
      }
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
      this.main = true
      setTimeout(() => {
        this.transform = true
      }, 2500)
      this.sub = false
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
        e.target.style.color = '#8AAAE5'
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

  $bg: #8AAAE5;
  // $bg:#DCE2F0;
  $color: #fefefe;
  $grColor:radial-gradient(circle, rgba(237,242,246,1) 8%, rgba(138,170,229,1) 78%);
  $boxFont:  'Cormorant SC', serif;
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
      // overflow-x: hidden;
      // background: rgb(237,242,246);
      background-image: $grColor;
  }

  body::-webkit-scrollbar {
      width: 8px;
      /* 스크롤바의 너비 */
  }

  body::-webkit-scrollbar-thumb {
      height: 30%;
      /* 스크롤바의 길이 */
      background: $bg;
      /* 스크롤바의 색상 */
      border-radius: 10px;
  }

  body::-webkit-scrollbar-track {
      background: #c7d3ee
          /*스크롤바 뒷 배경 색상*/
  }

  header {
      width: 100vw;
      // background-color: rgba($color: #323f6e, $alpha: 0.6);
      padding: 10px 0;
      position: fixed;
      z-index: 9;
      #header-cube{
          width: 3.4vw;
          transform:skewX(0deg);
          position: relative;
          border: none;
          &>a{
              width: 3.4vw;
              height: 3.4vw;
              position: absolute;
              top: 0;
              transform:skewX(0deg);
              animation: spin 5s infinite linear;
              transform-style: preserve-3d;
              font-family: $boxFont;
          }
          a>div {
              width: 3.4vw;
              height: 3.4vw;
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
              transform: rotateY(90deg) translateZ(1.7vw);
          }
          .two {
              transform: translateZ(1.7vw);
          }

          .three {
              transform: rotateY(-90deg) translateZ(1.7vw);
          }

          .four {
              transform: rotateX(90deg)translateZ(1.7vw);
          }

          .five {
              transform: rotateX(-90deg) translateZ(1.7vw);

          }

          .six {
              transform: rotateX(180deg) translateZ(1.7vw);

          }

      }
      ul {
          display: flex;
          justify-content: space-around;
          font-size: 1vw;
          li{
              width: 11vw;
              text-align: center;
              padding: 0.5vw 0;
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

  #loading {
      position: absolute;
      top: 0;
      background-color: #000000;
      width: 100vw;
      height: 100vh;
      // color:$color;
      &::after {
          content: '';
          text-align: center;
          width: 100%;
          // height: 50px;
          height: 20px;

          position: absolute;
          top: 50%;
          opacity: 1;
          transform: translateY(-50%);
          background-color: #fff;
          color: black;
          overflow: hidden;
          animation: load 1s linear;
      }
  }
  @keyframes load {
      0% {
          width: 0;
          height: 2px;
          opacity: 0;
      }
      50% {
          width: 100%;
          // display: n;
          opacity: 1;
          height: 2px;
      }
      100% {
          height: 20px;
          // top:0
      }
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
          // color:$bg;
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
          // perspective: 800;
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
              @keyframes scale2 {
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
                      animation: scale2 1.5s both;
                  animation-delay: 0.5s;
                  // animation-delay: 2s;

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
          }
          img {
              width: 100%;
              height: 100%;
          }
      }

  }
  .scale-enter-active,
  .scale-leave-active {
      transition: 1s linear;
      transform: scale(1);
  }
  .scale-enter,
  .scale-leave-to {
      opacity: 0;
      transform: scale(0.5)
  }
  .fade-enter-active,
  .fade-leave-active {
      animation: mainFadeIn 1s;
  }
  .fade-enter,
  .fade-leave-to {
      opacity: 0;
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
      height: 95%;
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
  #full {
      height: 100vh;
      display: flex;
      align-items: center;
      justify-content: space-around;
      position: relative;
      transition: all 0.6s;
      &>.full {
          width: 100vw;
          height: 100vh;
          transition: all 0.4s;
          overflow: hidden;
          &:not(:first-of-type){
              display: flex;
          }
          &>div{
              width: 100%;
              @include subBox
          }
      }

      #project {
          width: 500%;
          height: 100%;
          display: flex;
          align-items: center;
          cursor: grabbing;
          li {
              width: 20%;
              @include subBox;
              &>div{
                  display:flex;
                  &>div{
                  width: 50%;
                  // border: 1px solid #000;
                  img{
                      width: 100%;
                      height: 100%;
                  }
                }
             }
          }
      }
  }
  </style>

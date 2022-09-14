<template>
    <div id="full" v-show="sub" @wheel.prevent="subWheel">
      <div class="full" id="outer">
        <div id="wheel-left" @click="projectLeft"><img :src="wheelImg" alt="left" v-show="projectI>0"></div>
        <div id="wheel-right" @click="projectRight"><img :src="wheelImg" alt="right" v-show="projectI<projectPage.length-1"></div>
        <ul id="project" @mousedown="mDown" @mouseup="mUp" @mousemove="mMove">
          <li id="project1" class="moveI">
            <h2>{{navName[0]}}-1</h2>
            <div>
                <div class="project-img">
                  <img :src="projectImg[0]" alt="p0" @mouseover.stop="imgOver" @mouseout="imgOut">
                </div>
                <div class="project-text">
                  <div class="text-box">
                    음악을 주제로 만든 웹사이트입니다.<br>
                    svg 배경을 활용했으며 검정색 테마를 선정했습니다.<br>
                    Javascript, jquery를 활용하여
                    메인동영상의 길이에 따라 달라지는 재생바와 일지정지, 재생 버튼을 만들었으며,<br>
                    차트 부분에는 Json 파일과 ajax를 이용하여 차트를 불러오도록 하였습니다.<br>
                    오픈API를 모르던 상태로 작업을 시작하여 음악재생 및 재생목록을 구현 못한것이 아쉬워
                    추후에 기능을 추가해볼 생각입니다.<br>
                    반응형 : O
                  </div>
                  <div class="button-box">
                    <a :href="projectPage[0].main" target="_blank">Main</a>
                    <a :href="projectPage[0].sub" target="_blank">Sub</a>
                  </div>
                </div>
            </div>
          </li>
          <li class="moveI">
              <h2>{{navName[0]}}-2</h2>
              <div>
                <div class="project-img">
                  <img :src="projectImg[1]" alt="p1" @mouseover.stop="imgOver" @mouseout="imgOut">
                </div>
                <div class="project-text">
                  <div class="text-box">
                    공부서점사이트 클론코딩 프로젝트입니다.<br>
                    카카오API를 활용하여 작업을 진행하였고
                    api 활용하는것이 목적이었기 때문에 최대한 원래 사이트와 똑같이
                    구현해보려 했습니다.<br>
                    베스트 차트 부분에서는 Javascript의 이중배열을 활용하여
                    카테고리가 바뀔때마다 다른검색어로 검색이되어
                    카테고리마다 다른 책들이 보여지게 구현 하였습니다.<br>
                    서브페이지의 리뷰 부분에선 옵션선택에 따라 포토리뷰와 일반리뷰를
                    구분하여 볼 수 있도록 구현하였습니다.<br>
                    반응형 : X
                  </div>
                  <div class="button-box">
                    <a :href="projectPage[1].main" target="_blank">Main</a>
                    <a :href="projectPage[1].sub" target="_blank">Sub</a>
                  </div>
                </div>
              </div>
          </li>
          <li class="moveI">
              <h2>{{navName[0]}}-3</h2>
              <div>
                <div class="project-img">
                  <img :src="projectImg[2]" alt="p2" @mouseover.stop="imgOver" @mouseout="imgOut">
                </div>
                <div class="project-text">
                  <div class="text-box">
                    애견호텔을 주제로 만든 웹사이트입니다.<br>
                    jquery를 통해 스크롤값에 따라 각 섹션들이 보여지도록 구현했습니다.<br>
                    첫 반응형 작업을 한 사이트이며<br>
                    서브페이지에는 객실과 편의시설을 보여주는 페이지를 만들었습니다.<br>
                    반응형 : O
                  </div>
                  <div class="button-box">
                    <a :href="projectPage[2].main" target="_blank">Main</a>
                    <a :href="projectPage[2].sub" target="_blank">Sub</a>
                  </div>
                </div>
              </div>
          </li>
          <li class="moveI">
              <h2>{{navName[0]}}-4</h2>
              <div>
                <div class="project-img">
                  <img :src="projectImg[3]" alt="p3" @mouseover.stop="imgOver" @mouseout="imgOut">
                </div>
                <div class="project-text">
                  <div class="text-box">
                    에버랜드를 주제로 한 웹사이트이며 첫 팀프로젝트 작업입니다.<br>
                    총 4명이 팀으로 메인페이지와 서브 3페이지를 나누어 맡았으며
                    저는 메인페이지를 담당하였습니다.<br>
                    팀원들과 상의하며 모두 각각의 페이지를 만들 때 통일성을 중요시 여기며
                    공통된 UI요소를 정한 뒤에 작업을 시작하였습니다.<br>
                    스크롤 값에 따라 헤더의 배경색이 바뀌게 구현했으며,
                    css 애니메이션을 활용하여 동적인 사이트를 만들고자 하였습니다.<br>
                    반응형 : X
                  </div>
                  <div class="button-box">
                    <a :href="projectPage[3].main" target="_blank">Main</a>
                    <!-- <a :href="projectPage[3].sub" target="_blank">Sub</a> -->
                  </div>
                </div>
              </div>
          </li>
          <li class="moveI">
              <h2>{{navName[0]}}-5</h2>
              <div>
                <div class="project-img">
                  <img :src="projectImg[4]" alt="p4" @mouseover.stop="imgOver" @mouseout="imgOut">
                </div>
                <div class="project-text">
                  <div class="text-box">
                    HTML과 CSS를 배운후 처음으로 작업해본 웹사이트입니다.<br>
                    첫 프로젝트인 만큼 제가 가장 좋아하는 축구를 주제로 선정했으며
                    축구용품 사이트를 만들게 되었습니다.<br>
                    작업을 하면서 추가로 배우게 된 내용이 생길 때 마다
                    바로 프로젝트에 적용시켜보려했습니다.<br>
                    반응형 : X
                  </div>
                  <div class="button-box">
                    <a :href="projectPage[4].main" target="_blank">Main</a>
                    <a :href="projectPage[4].sub" target="_blank">Sub</a>
                  </div>
                </div>
              </div>
          </li>
        </ul>
      </div>
      <div class="full">
          <div class="full-sub">
              <h2>{{navName[1]}}</h2>
              <div id="about">
                <div id="aboutTop"><img :src="img[8]" alt="photo"></div>
                <div id="aboutBot">
                  <p>김동현</p>
                  <p>1998.12.10</p>
                  <p>경기도 안산시 거주</p>
                  <p>amawang@naver.com</p>
                  <p>2022.03 ~ 2022.09 라인컴퓨터아트학원 UI/UX 디자인 & 웹퍼블리셔 과정</p>
                  <p>웹디자인기능사</p>
                  <div>
                    신입 웹 퍼블리셔, 프론트엔드 개발자를 희망하는 김동현 입니다.<br>
                    현재에 만족하지않고 새로운 기술을 습득하는 것을 추구하며<br>
                    새로운 기술을 배울 때 작동원리를 알아낸 후 그것을 직접 구현하는 것에 흥미를 느낍니다.
                  </div>
                </div>
              </div>
          </div>
      </div>
      <div class="full">
          <div class="full-sub">
              <h2>{{navName[2]}}</h2>
              <div id="skill">
                <div>
                  <div><img :src="img[0]" alt="html"></div>
                  <div><img :src="img[1]" alt="css"></div>
                  <div><img :src="img[2]" alt="js"></div>
                  <div><img :src="img[3]" alt="jquery"></div>
                </div>
                <div>
                  <div><img :src="img[4]" alt="ajax"></div>
                  <div><img :src="img[5]" alt="sass"></div>
                  <div><img :src="img[6]" alt="vue"></div>
                  <div><img :src="img[7]" alt="github"></div>

                </div>
              </div>
          </div>
      </div>
      <div class="full">
          <div class="full-sub">
              <h2>{{navName[3]}}</h2>
              <div id="contact">
                <div>
                  <div class="front">
                    <p>H.P</p>
                  </div>
                  <div class="back"><input type="text" v-model="hp" disabled></div>
                </div>
                <div>
                  <div class="front">
                    <p>E-mail</p>
                  </div>
                  <div class="back"><input type="text" value="amawang@naver.com" disabled></div>
                </div>
                <div>
                  <div class="front">GitHub</div>
                  <div class="back">https://github.com/kimddddh98</div>
                </div>
              </div>
          </div>
      </div>
      <div class="full">
          <div class="full-sub">
              <h2>{{navName[4]}}</h2>
              <div id="more">
                <div>
                  웹 사이트를 만드는 것은 저에게 상상할 수 없던 일이었습니다.<br>
                  하지만 꾸준한 학습으로 여러 사이트를 만들게 되었습니다.<br>
                  처음 html,css를 배울때처럼 앞으로도 새로운 것을 학습하는 것을<br>
                  두려워하지않고 제 것으로 만들것이며<br>
                  현재의 나보다 더 나은 개발자가 되는 것을 목표로 할 것 입니다.
                </div>
                <h2>THANK YOU FOR WATCHING !</h2>

              </div>
          </div>
      </div>
    </div>

</template>
<script>
export default {
  props: {
    navName: Array,
    sub: Boolean,
    circleStyle: Array
  },
  data () {
    return {
      press: false,
      startx: null,
      up: null,
      projectI: 0,
      img: [
        require('@/assets/html.png'),
        require('@/assets/css.png'),
        require('@/assets/js.png'),
        require('@/assets/jquery.png'),
        require('@/assets/ajaxicon.svg'),
        require('@/assets/sass.png'),
        require('@/assets/vue.png'),
        require('@/assets/github.png'),
        require('@/assets/kim.jpg')
      ],
      projectImg: [
        require('@/assets/music.png'),
        require('@/assets/ajax.png'),
        require('@/assets/dogroom.png'),
        require('@/assets/everland.png'),
        require('@/assets/ezsoccer.png')
      ],
      wheelImg: require('@/assets/left.png'),
      hp: '010-4252-3496',
      mainPage: 'https://kimddddh98.github.io/project3/',
      subPage: 'https://kimddddh98.github.io/project3/sub.html',
      projectPage: [
        { main: 'https://kimddddh98.github.io/project3/', sub: 'https://kimddddh98.github.io/project3/sub.html' },
        { main: 'https://kimddddh98.github.io/project4_ajax/', sub: 'https://kimddddh98.github.io/project4_ajax/sub.html' },
        { main: 'https://kimddddh98.github.io/project2/', sub: 'https://kimddddh98.github.io/project2/sub.html' },
        { main: 'https://kimddddh98.github.io/team_project/' },
        { main: 'https://kimddddh98.github.io/project1/', sub: 'https://kimddddh98.github.io/project1/sub.html' }

      ]
    }
  },
  methods: {
    projectLeft () {
      const innerUl = document.querySelector('#project')
      if (this.projectI > 0) {
        this.projectI--
        innerUl.style.transition = '0.5s'
        innerUl.style.marginLeft = -100 * this.projectI + 'vw'
      }
    },
    projectRight () {
      const innerUl = document.querySelector('#project')
      if (this.projectI < this.projectPage.length - 1) {
        this.projectI++
        innerUl.style.transition = '0.5s'
        innerUl.style.marginLeft = -100 * this.projectI + 'vw'
      }
    },
    imgOut (e) {
      e.target.style.top = 0
      e.target.style.transition = 'none'
    },
    imgOver (e) {
      const pNode = e.target.parentNode.offsetHeight
      e.target.style.transition = '5s linear'
      e.target.style.top = -(e.target.offsetHeight - pNode) + 'px'
    },
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
      innerUl.style.cursor = 'grab'
      innerUl.style.transition = '0.5s'
      if (this.up < 0) {
        this.projectI++
        innerUl.style.marginLeft = -100 * this.projectI + 'vw'
        this.up = null
      } else if (this.up > 0) {
        this.projectI--
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
        this.up = document.querySelectorAll('.moveI')[this.projectI].offsetLeft
      }
    }
  }
}
</script>

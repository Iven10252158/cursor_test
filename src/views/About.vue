<template>
  <div class="about" ref="about">
    <div class="mouse-icon" ref="mouseIcon" @mousemove="handleMouse" :style="{left: mouseX + 'px', top: mouseY + 'px'}">
      <div ref="circle" class="circle border border-5" :class="{'border border-success': cursor_color_green, 'border border-danger': cursor_color_red}"></div>
        <div class="circle-heart" ref="circleHeart" v-if="cursor_status === 'drag'"
        :class="{'bg-primary': is_transparent}"></div>
        <div class="circle-heart" ref="circleHeart" v-if="cursor_status === 'scroll'"
        :class="{'bg-success': is_transparent}"></div>
        <div class="circle-heart" ref="circleHeart" v-if="cursor_status === 'click'"
        :class="{'bg-fa0': is_transparent}"></div>
      </div>
    <h1 class="main-text" ref="mainText">This is an about page</h1><br>
    <h2>座標 {{ mouseX }}/{{mouseY}}</h2>
    <button type="button" class="click" @click="click">click</button>
  </div>
</template>

<script>
import { connectSocket, connectSocketTouch } from '@/webSocket/websocket'
export default {
  data () {
    return {
      mouseX: 0,
      mouseY: 0,
      circleW: 0,
      circleH: 0,
      circleHeartW: 0,
      circleHeartH: 0
    }
  },
  watch: {
    cursor_rate () {
      this.$refs.circle.style.width = (this.cursor_rate * 70) + 40 + 'px'
      this.$refs.circle.style.height = (this.cursor_rate * 70) + 40 + 'px'
      console.log('watch', this.$refs.circle.style.width)
      // this.$refs.circle.style.transform = `scale(${this.cursor_rate})`
      // console.log('watch', this.cursor_rate)
    }
  },
  computed: {
    cursor_color_green () {
      return this.$store.getters['cursorState/cursor_color_green']
    },
    cursor_color_red () {
      return this.$store.getters['cursorState/cursor_color_red']
    },
    is_transparent () {
      return this.$store.getters['cursorState/is_transparent']
    },
    cursor_status () {
      return this.$store.getters['cursorState/cursor_status']
    },
    cursor_rate () {
      return this.$store.getters['cursorState/cursor_rate']
    }
  },
  methods: {
    handleMouse (event) {
      // console.log(window.innerHeight)
      // 外框尺寸
      this.circleW = this.$refs.circle.offsetWidth
      this.circleH = this.$refs.circle.offsetHeight
      this.mouseX = event.clientX - 50
      this.mouseY = event.clientY - 50
      const mouseLeft = window.innerWidth - this.circleW
      const mouseTop = window.innerHeight - this.circleH
      if (this.mouseX > mouseLeft) {
        this.mouseX = mouseLeft
      } else if (this.mouseY > mouseTop) {
        this.mouseY = mouseTop
      }
      // this.$refs.mouseIcon.classList.remove('transition')
    },
    rate () {
      // this.$refs.circle.style.transform = `scale(${this.cursor_rate})`
      this.$refs.circle.style.width = (this.cursor_rate * 70) + 40 + 'px'
      this.$refs.circle.style.height = (this.cursor_rate * 70) + 40 + 'px'
      console.log('width', this.$refs.circle.style.width)
    },
    click () {
      console.log('click')
    }
  },
  mounted () {
    connectSocket()
    connectSocketTouch()
    document.addEventListener('mousemove', this.handleMouse)
    this.rate()
  }
}
</script>

<style lang="scss" scoped>
*{
  box-sizing: border-box;
}
.about{
  border: 2px solid;
  // height: 90vh;
}
.main-text{
  display: inline-block;
  border: 1px solid;
  background-color: #fa0;
}
.mouse-icon{
  position: absolute;
  transform: scale(1);
  transition: transform 1s;
}
.transition {
  transform: scale(0.5);
  transition: transform 1s;
}

.circle{
  width: 100px;
  height: 100px;
  border: 5px solid #000;
  border-radius: 50%;
  position: relative;
  z-index: 5;
}
.circle-heart{
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%);
  width: 30px;
  height: 30px;
  background-color: #fa0;
  border-radius: 50%;
  z-index: 5;
}
.circle-transparent {
  opacity: 0;
}
.bg-fa0{
  background-color: #fa0;
}
</style>

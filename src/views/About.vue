<template>
  <div class="about" ref="about">
    <div class="mouse-icon" ref="mouseIcon" @mousemove="handleMouse" :style="{left: mouseX + 'px', top: mouseY + 'px'}">
      <div ref="box" class="box"></div>
    </div>
    <h1 class="main-text" ref="mainText">This is an about page</h1><br>
    <h2>座標 {{ mouseX }}/{{mouseY}}</h2>
    <button type="button" class="click" @click="click">click</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      mouseX: 0,
      mouseY: 0
      // mouseLeft: 0,
      // mouseTop: 0
    }
  },
  methods: {
    handleMouse (event) {
      // console.log(window.innerHeight)
      this.mouseX = event.clientX
      this.mouseY = event.clientY
      const mouseLeft = window.innerWidth - 30
      const mouseTop = window.innerHeight - 30
      // console.log(mouseTop)
      if (this.mouseX > mouseLeft) {
        this.mouseX = mouseLeft
      } else if (this.mouseY > mouseTop) {
        this.mouseY = mouseTop
      }
      // console.log('mouseLeft', this.mouseLeft, 'mouseX', this.mouseX)

      this.$refs.mouseIcon.classList.remove('transition')
    },
    click (event) {
      this.$refs.mouseIcon.classList.add('transition')
      console.log('click', event)
    }
  },
  mounted () {
    document.addEventListener('mousemove', this.handleMouse)
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
.box{
  position: absolute;
  width: 30px;
  height: 30px;
  border: 5px solid #fa0;
  border-radius: 50%;
}
</style>

<template>
  <div class="about"  @mousemove="handleMouse">
    <div class="mouse-icon" ref="mouseIcon" :style="{left: mouseX + 'px', top: mouseY + 'px'}">
      <div class="box"></div>
    </div>
    <h1 class="main-text" ref="mainText">This is an about page</h1><br>
    <h2>滑鼠座標 {{ mouseX }}/{{mouseY}}</h2>
    <button type="button" class="click" @click="click">click</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      mouseX: 0,
      mouseY: 0,
      textH: 0,
      textW: 0
    }
  },
  methods: {
    handleMouse () {
      document.onmousemove = (event) => {
        this.mouseX = event.clientX
        this.mouseY = event.clientY
        this.$refs.mouseIcon.classList.remove('transition')
      }
    },
    click () {
      // document.onmousemove = (event) => {
      this.$refs.mouseIcon.classList.add('transition')
      // }
      console.log('click')
    }
  },
  mounted () {
  }
}
</script>

<style lang="scss" scoped>
.main-text{
  display: inline-block;
  border: 1px solid;
  background-color: #fa0;
}
.mouse-icon{
  position: absolute;
  z-index: 1;
  transform: scale(1);
  transition: transform 1s;
  img {
    width: 50px;
  }
}
// .click{
//   position: relative;
//   z-index: 2;
// }
.transition {
  transform: scale(0.5);
  transition: transform 1s;
}
.box{
  width: 25px;
  height: 25px;
  border: 5px solid #fa0;
  border-radius: 50%;
}
</style>

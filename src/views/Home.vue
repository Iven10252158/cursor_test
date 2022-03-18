<template>
  <div class="home" @mousemove="mousePosition">
    X座標:{{ pageX }}
    Y座標:{{ pageY }}
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  components: {
    HelloWorld
  },
  data () {
    return {
      pageX: 0,
      pageY: 0
    }
  },
  methods: {
    mousePosition (event) {
      this.pageX = event.pageX
      this.pageY = event.pageY
      console.log(event)
    }
  },
  mounted () {
  }
}
</script>

<style scoped>
  .icon{
    height: 50px;
    width: 50px;
    background-color: #fa0;
  }
  .pointer {
    cursor: pointer
  }
  .wait{
    cursor: wait
  }
</style>

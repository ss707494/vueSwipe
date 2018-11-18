<template>
  <div id="app">
      <Swipe ref="swipe" class="swipe">
        <div
            class="item"
        >
          <img src="./assets/images.jpg"
               alt="">
        </div>
        <div
            class="item"
        >
          <img src="./assets/images2.jpg"
               alt="">
        </div>
        <div
            class="item"
        >
          <img src="./assets/images3.jpg"
               alt="">
        </div>
      </Swipe>
    <div>
      <button @click="pre" >pre</button>
      <button @click="next" >next</button>
      <!--{{this.activeNum}}-->
    </div>
  </div>
</template>
<style lang="scss">
  .swipe {
    height: 640px;
  }
  .item {
    img {
      width: 100%;
      height: 100%;
    }
  }
</style>

<script>
import Swipe from './components/Swipe'

export default {
  name: 'app',
  components: {
    Swipe,
  },
  methods: {
    pre() {
      this.$refs.swipe.pre()
    },
    next() {
      this.$refs.swipe.next()
    }
  }
}
</script>

<style>
    * {
        padding: 0;
        margin: 0;
    }
</style>

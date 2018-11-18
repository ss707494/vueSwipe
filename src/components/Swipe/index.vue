<template>
  <div class="m-swipe">
    <div class="m-swipe-container">
      <div
          ref="wraps"
          class="m-swipe-wrap"
          :style="calcStyle"
      >
        <slot/>
      </div>
    </div>
    <slot name="indicator">
      <div class="m-swipe-indicators">
        <i
            v-for="index in itemLength"
            class="m-swipe-indicator"
            :key="`indicator${index}`"
            :class="index -1 === activeNum ? 'm-swipe-indicator__active' : ''"
            @click="move(index - 1)"
        />
      </div>
    </slot>
  </div>
</template>
<style lang="scss"
       src="./index.scss">
</style>
<script>
  export default {
    props: {
      speed: {
        type: Number,
        default: 2000
      },
    },
    data() {
      return {
        items: [],
        duration: 2000,
        activeNum: 1,
        itemLength: 3,
        offset: 0,
      }
    },
    computed: {
      calcStyle() {
        return {
          'transform': `translate3d(calc(-${this.activeNum + 1}00% + ${this.offset}px),0,0)`,
          'transition-duration': this.duration + 'ms'
        }
      },
    },
    mounted() {
      this.items = this.$refs.wraps.children
      this.itemLength = this.items.length
      this.createLoopEl()
    },
    methods: {
      move(n) {
        this.activeNum = n
      },
      next() {
        // this.$refs.wraps.getPropertyValue
        // debugger
        // setInterval(() => {
        //   console.log()
        // }, 200)
        if (this.activeNum === this.itemLength - 1) {
          this.duration = 0
          this.activeNum = -1
          setTimeout(() => {
            this.duration = this.speed
            this.activeNum = 0
          }, 100)
        } else {
          this.activeNum += 1
        }
      },
      pre() {
        if (this.activeNum === 0) {
          this.duration = 0
          this.activeNum = this.itemLength
          setTimeout(() => {
            this.duration = this.speed
            this.activeNum = this.itemLength - 1
          }, 100)
        } else {
          this.activeNum -= 1
        }
      },
      createLoopEl() {
        var swiperWrapEl = this.$refs.wraps;
        var duplicateFirstChild = swiperWrapEl.firstElementChild.cloneNode(true);
        var duplicateLastChild = swiperWrapEl.lastElementChild.cloneNode(true);
        swiperWrapEl.insertBefore(duplicateLastChild, swiperWrapEl.firstElementChild);
        swiperWrapEl.appendChild(duplicateFirstChild);
      }
    }
  }
</script>


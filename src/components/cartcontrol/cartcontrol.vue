<template>
 <div class="cartcontrolBox">
  <transition name="rotate">
    <div class="jian" @click.stop.prevent="decreaseCart" v-show="footlook.count>0">-</div>
  </transition>
   <div class="shu" v-show="footlook.count>0">{{footlook.count}}</div>
   <div class="jia" @click.stop.prevent="addCart">+</div>
 </div>
</template>

<script type="text/ecmascript-6">
  import Vue from 'vue'
  export default {
    props: {
      footlook: {
        type: Object
      }
    },
    created () {
      console.log(this.footlook)
    },
    methods: {
      addCart (event) {
        if (!event._constructed) {
          return
        }
        if (!this.footlook.count) {
          Vue.set(this.footlook, 'count', 1)
        } else {
          this.footlook.count++
        }
      },
      decreaseCart (event) {
        if (!event._constructed) {
          return
        }
        if (this.footlook.count) {
          this.footlook.count--
        }
      }
    }
  }
</script>
<style lang="stylus" rel="stylesheet/stylus">
.cartcontrolBox 
  display: inline-block
  position: absolute
  bottom: 0
  right: 0
  text-align: center
  display: flex
  .shu
    line-height: 24px
    height: 24px
    padding: 0 12px
  .jia
    width: 24px
    height: 24px
    font-size: 24px
    background: #00a0dc
    border-radius: 50%
    font-weight: bold
    color: #fff
  .jian
    width: 24px
    height: 24px
    font-size: 24px
    background: #00a0dc
    border-radius: 50%
    font-weight: bold
    color: #fff
    transition: all 0.4s linear
    &.rotate-transition
      opacity: 1
      transform: rotate(0)
    &.rotate-enter, &.rotate-leave
      opacity: 0
      transform: rotate(180deg)
</style>


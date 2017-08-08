<style lang="stylus" rel="stylesheet/stylus">
@import "../../assets/stylus/mixin.styl"
.payBox
  position: fixed
  width: 100%
  top: 0
  height: 100%
  background:#000
  -webkit-animation:fadeInRight 0.5s .1s ease both
  -moz-animation:fadeInRight 0.5s .1s ease both
  @-webkit-keyframes fadeInRight{
    0%{
      -webkit-transform:translateX(100%)
  }
    100%{
      -webkit-transform:translateX(0)
  }
  }
  @-moz-keyframes fadeInRight{
    0%{
      -moz-transform:translateX(100%)
    }
    100%{
      -moz-transform:translateX(0)
    }
  }
  .blueImg
    width:100%
    position: absolute
    top: 50%
    transform: translateY(-50%)
    >img
      width: 100%
  .payContainer
    background:#FB3243
    width: 300px
    position: fixed
    left: 50%
    top: 50%
    transform: translate(-50%,-50%)
    color: #EEECBB
    text-align: center
    padding: 5px 0 10px 0
    border-radius: 7px
    .payHead
      font-size: 22px
      font-weight: 700
      line-height: 50px
      position: relative
      .guanbi{
        font-size: 20px
        position: absolute
        left: 0
        padding: 0 20px 
      }
    .payLogo
      .paylogoImg
        border-radius: 50%
    .payBorder
      position: relative
      .borderLeft
        width: 160px
        height: 4px
        background: #eeecbb
        position: absolute
        left: -5px
        top: -15px;
        transform: rotate(20deg)
      .borderRight
        width: 160px
        height: 4px
        background: #eeecbb
        position: absolute
        right: -5px
        top: -15px;
        transform: rotate(-20deg)
    .payMoney
      margin: 15px 0
      .getMoney
        font-size: 50px
        line-height: 50px
        font-weight: 700
        display: inline-block
        padding-right: 5px
    .payText
      font-size: 12px
      margin-top: 10px
      height: 20px
    .payBottom
      .pay
        width: 80%
        background:#eeecbb
        color: #c33924
        border-radius: 10px
        font-size: 18px
        line-height: 40px
        font-weight: bold
        margin: 10px auto
      .meTo
        width: 80%
        color: #eeecbb
        border-radius: 10px
        font-size: 18px
        line-height: 40px
        font-weight: bold
        border: solid 1px #eeecbb
        margin: 10px auto

</style>
<template>
  <div class="payBox" v-show="showFlag">
    <div class="blueImg">
      <img id="c_img" src="./4.jpg" alt="" />
    </div>
    <div class="payContainer">
        <div class="payHead"><span class="guanbi" @click="close()">X</span>打赏看视频</div>
        <div class="payLogo"><img class="paylogoImg" src="./2.jpg" width="50" height="50" alt="" /></div>
        <div class="payBorder">
          <span class="borderLeft"></span>
          <span class="borderRight"></span>
        </div>
        <div class="payMoney"><span class="getMoney">{{pay.money}}</span>元</div>
        <div class="introText">打赏看视频</div>
        <div class="payText">（内容由用户发布，并非平台提供，赏金归发布者）</div>
        <div class="payBottom">
          <div class="pay">打赏</div>
          <div class="meTo">我也要生成</div>
        </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    pay: {
      type: Object
    }
  },
  data () {
    return {
      showFlag: false
    }
  },
  methods: {
    cc (mag) {
      console.log(mag)
    },
    show () {
      console.log('111111111')
      this.showFlag = true
    },
    close () {
      console.log('222222')
      this.showFlag = false
    }
  },
  computed: {
  },
  components: {
  }
}

</script>

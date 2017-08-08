<template>
  <div class="showcartBox">
    <div class="cart">
      <div class="cartlogo">
        <div class="cartiocn" :class="logoheight"><img src="./cart.png" height="24" width="24" alt="" /></div>
        <div class="num" v-show="morecount>0">{{morecount}}</div>
      </div>
      <div class="cartmoney">
        <span class="money">￥{{totalPrice}}</span>
        <span>另需配送费￥{{deliveryPrice}}元</span>
      </div>
    </div>
    <div class="buymoney" @click.stop.prevent="postMoney">
      <div class="moneyText" :class="heightclass">{{moneyPay}}</div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    selectFoods: {
      type: Array,
      default () {
        return [
          {
            price: 10,
            count: 3
          }
        ]
      }
    },
    deliveryPrice: {
      type: Number,
      default: 0
    },
    minPrice: {
      type: Number,
      default: 0
    }
  },
  data () {
    return {
    }
  },
  mounted () {
  },
  computed: {
    totalPrice () {
      let total = 0
      this.selectFoods.forEach((food) => {
        total += food.price * food.count
      })
      return total
    },
    morecount () {
      let numcount = 0
      this.selectFoods.forEach((food) => {
        numcount += food.count
      })
      return numcount
    },
    moneyPay () {
      if (this.totalPrice === 0) {
        return `还差${this.minPrice}元起送`
      } else if (this.totalPrice < this.minPrice) {
        let deff = this.minPrice - this.totalPrice
        return `还差${deff}起送`
      } else {
        return '去结算'
      }
    },
    logoheight () {
      if (this.morecount > 0) {
        return 'logoheight'
      } else {
        return
      }
    },
    heightclass () {
      if (this.totalPrice < this.minPrice) {
        return 'no-height'
      } else {
        return 'height'
      }
    }
  },
  methods: {
    postMoney () {
      if (this.totalPrice < this.minPrice) {
        return
      }
      window.alert(`支付${this.totalPrice}元`)
    }
  },
  components: {}
}
</script>
<style lang="stylus" rel="stylesheet/stylus">
.showcartBox
  position: fixed
  width: 100%
  bottom: 0
  height: 48px
  background: #141d27
  display: flex
  .cart
    flex:1
    position: relative
    .cartlogo
      width: 55px
      height: 55px
      display: inline-block
      background: #141d27
      border-radius: 50%
      position: absolute
      left: 18px
      bottom: 8px
      text-align: center
      .cartiocn
        width: 45px
        height: 45px
        display: inline-block
        background: #2b343c
        border-radius: 50%
        margin-top: 5px
        line-height: 55px
        &.logoheight
          background: #00a0dc
      .num
        position: absolute
        width: 24px
        height: 16px
        background: red
        color: #fff
        fonz-weight: 700
        top: 0
        right: 0
        border-radius: 10px
        font-size: 12px
        line-height: 16px
        text-align: center
    .cartmoney
      color: rgba(255,255,255,0.4)
      font-weight: 700
      font-size: 10px
      padding-left: 70px
      line-height: 48px
      .money
        font-size: 16px
        font-weight: 700
        border-right:1px solid rgba(255,255,255,0.1)
        padding: 5px 12px 5px 18px
        margin-right: 12px
  .buymoney
    flex: 0 0 105px
    .moneyText
      font-size: 12px
      color: rgba(255,255,255,0.4)
      font-weight: 700
      line-height: 48px
      text-align: center
      &.no-height
        background: #2b343c
      &.height
        background: #00b43c
        color: #fff
</style>


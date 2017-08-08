<template>
  <div class="sellerBox">
    <div class="sellerMenu" ref="sellerMenu">
      <ul>
        <li class="mentItem" v-for="(item,index) in goods" @click="selectMenu(index,$event)" :class="{'current':currentIndex===index}">
          <span class="menuName cc">{{item.name}}</span>
        </li>
      </ul>
    </div>
    <div class="sellerfoot" ref="sellerfoot">
      <ul>
        <li v-for="item in goods" class="ww">
          <div class="footName">{{item.name}}</div>
          <ul>
            <li class="footlookLi" v-for="footlook in item.foods">
              <div class="footlookBox">
                <div class="footlookImg"><img :src="footlook.image" width="57" height="57" alt="" /></div>
                <div class="footlooknameBox">
                  <div class="footlookName">{{footlook.name}}</div>
                  <div class="footlookDescription" v-if="footlook.description">{{footlook.description}}</div>
                  <div class="footlooksellCount">月售{{footlook.sellCount}}<span class="footlookrating">好评率{{footlook.rating}}%</span></div>
                  <div class="footlookMoney">￥{{footlook.price}}<span class="moneyoldPrice" v-if="footlook.oldPrice">￥{{footlook.oldPrice}}</span></div>
                </div>
                <Cartcontrol :footlook="footlook"></Cartcontrol>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
    <Showcart :deliveryPrice="seller.deliveryPrice" :minPrice="seller.minPrice" :selectFoods="selectFoods"></Showcart>
  </div>
</template>

<script>
import BScroll from 'better-scroll'
import Showcart from '../../components/showcart/showcart.vue'
import Cartcontrol from '../../components/cartcontrol/cartcontrol.vue'
export default {
  data () {
    return {
      goods: [],
      seller: [],
      listHeight: [],
      scrollY: 0
    }
  },
  mounted () {
    this.getDate()
  },
  computed: {
    currentIndex () {
      for (let i = 0; i < this.listHeight.length; i++) {
        let height1 = this.listHeight[i]
        let height2 = this.listHeight[i + 1]
        if (!height2 || (this.scrollY >= height1 && this.scrollY < height2)) {
          return i
        }
      }
      return 0
    },
    selectFoods () {
      let foods = []
      this.goods.forEach((good) => {
        good.foods.forEach((food) => {
          if (food.count) {
            foods.push(food)
          }
        })
      })
      return foods
    }
  },
  methods: {
    getDate () {
      this.$http.get('static/data/data.json').then((res) => {
        console.log(res.data.goods)
        this.goods = res.data.goods
        this.seller = res.data.seller
        this.$nextTick(() => {
          this._BScroll()
          this._calculateHeight()
        })
      })
    },
    selectMenu (index, event) {
      if (!event._constructed) {
        return
      }
      let foodList = this.$refs.sellerfoot.getElementsByClassName('ww')
      let el = foodList[index]
      this.footScroll.scrollToElement(el, 300)
    },
    _BScroll () {
      this.meunScroll = new BScroll(this.$refs.sellerMenu, {
        click: true,
        probeType: 3
      })
      this.footScroll = new BScroll(this.$refs.sellerfoot, {
        click: true,
        probeType: 3
      })
      this.footScroll.on('scroll', (pos) => {
        this.scrollY = Math.abs(Math.round(pos.y))
      })
    },
    _calculateHeight () {
      let foodList = this.$refs.sellerfoot.getElementsByClassName('ww')
      let height = 0
      this.listHeight.push(height)
      for (let i = 0; i < foodList.length; i++) {
        let item = foodList[i]
        height += item.clientHeight
        this.listHeight.push(height)
      }
    }
  },
  components: {
    Showcart,
    Cartcontrol
  }
}

</script>
<style lang="stylus" rel="stylesheet/stylus">
.sellerBox
  display: flex
  position: absolute
  overflow: hidden
  top: 175px
  bottom: 48px
  width: 100%
  .sellerMenu
    flex: 0 0 80px
    background: #f3f5f7
    .mentItem
      padding: 0 12px
      &.current
        background: #fff
        margin-top: -1px
        >.cc
          border-bottom: none
      .menuName
        display: table-cell
        vertical-align: middle
        font-size: 12px
        line-height: 16px
        font-weight: 200
        color: #000
        height: 54px
        width: 56px
        border-bottom: solid 1px rgba(7,17,27,0.1)
  .sellerfoot
    flex: 1
    .footName
      font-size: 12px
      color: rgb(147,153,149)
      background: #f3f5f7
      line-height: 26px
      height: 26px
      padding-left: 14px
      border-left: solid 2px #d9dde1
    .footlookLi
      margin: 18px 18px 0 18px
      padding-bottom: 18px
      background: #fff
      border-bottom: solid 1px rgba(7,17,27,0.1)
      .footlookBox
        display: flex
        position: relative
        .footlookImg
          flex: 0 0 57px
          padding-right: 10px
        .footlookName
          font-size: 14px
          line-height: 14px
          color: rgb(7,17,27)
        .footlookDescription
          font-size: 10px
          line-height: 12px
          margin-top: 8px
          color: rgb(147,159,159)
        .footlooksellCount
          font-size: 10px
          line-height: 12px
          margin-top: 8px
          color: rgb(147,159,159)
          .footlookrating
            margin-left: 12px
        .footlookMoney
          font-size: 14px
          font-weight: 700
          line-height: 24px
          color: red
          .moneyoldPrice
            font-size: 10px
            color: rgb(147,159,159)
            font-weight: 700
            margin-left: 8px
            text-decoration:line-through
</style>


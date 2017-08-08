<template>
  <div class="header-box">
    <div class="header-background">
      <img :src="sellerHead.avatar" alt="" />
    </div>
    <div class="header">
      <div class="header-logo"><img :src="sellerHead.avatar" width="64" height="64" alt="" /></div>
      <div class="header-text">
        <div class="header-name"><i class="name-brand"></i>{{sellerHead.name}}</div>
        <div class="header-song">{{sellerHead.description}}/{{sellerHead.deliveryTime}}分钟送达</div>
        <div class="header-man" v-if="sellerHead.supports"><i class="man-ioc"></i>{{sellerHead.supports[0].description}}</div>
      </div>
      <div class="header-huo-length" v-if="sellerHead.supports" @click="detailTrue()">{{sellerHead.supports.length}}个<i class="header-huo-you"></i></div>
    </div>
    <div class="header-gong">
      <i class="header-gong-gao"></i>
      <span class="header-gong-text">{{sellerHead.bulletin}}</span>
      <i class="header-you"></i>
    </div>
    <transition name="fade">
      <div class="detail" v-show="detailShow">
        <div class="detail-box">
          <div class="detail-name">{{sellerHead.name}}</div>
          <div class="detail-star">
            <el-rate
              v-model="sellerHead.score"
              disabled
              text-color="#ff9900">
            </el-rate>
          </div>
          <div class="detail-youhui">
            <div class="detail-youhui-name">
              <i class="detail-youhui-hr"></i>
              <span class="detail-youhui-title">优惠信息</span>
              <i class="detail-youhui-hr"></i>
            </div>
            <div class="detail-youhui-ul" v-if="sellerHead.supports">
              <ul>
                <li v-for="item in sellerHead.supports">
                  <i class="liioc" :class="classMap[item.type]"></i>
                  <span class="detail-youhui-text">{{item.description}}</span>
                </li>
              </ul>
            </div>
          </div>
          <div class="detail-gonggao">
            <div class="detail-gaoggao-name">
              <i class="detail-gaoggao-hr"></i>
              <span class="detail-gaoggao-title">优惠信息</span>
              <i class="detail-gaoggao-hr"></i>
            </div>
            <div class="detail-gonggao-text">{{sellerHead.bulletin}}</div>
          </div>
        </div>
        <div class="guanbi">
          <i class="guanbi-ioc" @click="detailFalse()"></i>
        </div>
      </div>
    </transition>
  </div>
</template>

<script type="text/babel">
export default {
  data () {
    return {
      sellerHead: {},
      detailShow: false
    }
  },
  mounted () {
    this.getDate()
  },
  created () {
    this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
  },
  methods: {
    getDate () {
      this.$http.get('static/data/data.json').then((res) => {
        // console.log(res.data.seller)
        this.sellerHead = res.data.seller
      })
    },
    detailTrue () {
      this.detailShow = true
    },
    detailFalse () {
      this.detailShow = false
    }
  },
  components: {
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
.header-box
  overflow: hidden
  position: relative
  background: rgba(7, 17, 27, 0.5)
  .header-background
    position: absolute
    width: 100%
    overflow: hidden
    z-index: -1
    filter: blur(10px)
    img
      width: 100%
  .header
    display: flex
    padding: 24px 12px 18px 24px
    position: relative
    .header-logo
      flex: 0 0 64px
      display: inline-block
      margin-right: 16px
      img
        display: block
        border-radius: 2px
    .header-text
      flex: 1
      display:inline-block
      vertical-align: top
      color: #fff
      .header-name
        font-size: 16px
        font-weight: bold
        line-height: 18px
        .name-brand
          background: url('./brand@2x.png')
          background-size: 100% 100%
          width: 30px
          height: 18px
          display: inline-block
          vertical-align: top
          margin-right: 6px
      .header-song
        font-size: 12px
        padding: 8px 0 10px 0
        line-height: 12px
        font-weight: 200
      .header-man
        font-size: 10px
        font-weight: 200
        line-height: 12px
        .man-ioc
          width: 12px
          height: 12px
          background: url('./decrease_1@2x.png')
          display: inline-block
          background-size: 100% 100%
          vertical-align: top
          margin-right: 4px
    .header-huo-length
      position: absolute
      background: rgba(0,0,0,0.2)
      bottom: 12px
      right: 12px
      color: #fff
      font-size: 10px
      padding: 7px 8px
      border-radius: 10px
      .header-huo-you
        width: 12px
        height: 12px
        display: inline-block
        vertical-align: top
        background: url('./header-you.png')
        background-size: 100% 100%
  .header-gong
    color: #fff
    font-size: 10px
    font-weight: 200
    line-height: 28px
    padding: 0 22px 0 12px
    position: relative
    white-space: nowrap
    text-overflow: ellipsis
    overflow: hidden
    background-color: rgba(7, 17, 27, 0.2)
    .header-gong-gao
      width: 22px
      height: 12px
      display: inline-block
      background: url('./bulletin@2x.png')
      background-size: 100% 100%
      vertical-align: middle
    .header-gong-text
      vertical-align: top
    .header-you
      position: absolute
      right: 12px
      top: 8px
      width: 12px
      height: 12px
      display: inline-block
      background: url('./header-you.png')
      background-size: 100% 100%
  .detail
    position: fixed
    width: 100%
    height: 100%
    top: 0
    left: 0
    color: #fff
    text-align: center
    background: rgba(7, 17, 27, 0.8)
    z-index: 30
    &.fade-enter-active, &.fade-leave-active
      transition: opacity .5s
    &.fade-enter, &.fade-leave-to
      opacity: 0
    .detail-box
      margin-top: 64px
      .detail-name
        font-size: 16px
        font-weight: 700
        line-height: 16px
      .detail-star
        margin-top: 16px
        .el-rate
          height: 24px
          .el-rate__item
            margin: 0 8px
            .el-rate__icon
             font-size: 24px
      .detail-youhui
        .detail-youhui-name
          margin: 28px 36px
          position: relative
          display: flex
          .detail-youhui-hr
            width: 100%
            flex: 1
            height: 2px
            display: block
            top: 8px
            position: relative
            background: rgba(255, 255, 255, 0.2)
          .detail-youhui-title
            font-size: 16px
            font-weight: 700
            line-height: 16px
            padding: 0 12px
        .detail-youhui-ul
          text-align: left
          font-size: 12px
          font-weight: 200
          line-height: 12px
          margin: 28px 48px
          li
            margin: 12px 0
            .liioc
              width: 16px
              height: 16px
              display: inline-block
              vertical-align: middle
              &.decrease
                background: url('./decrease_1@2x.png')
                background-size: 100% 100%
              &.discount
                background: url('./discount_1@2x.png')
                background-size: 100% 100%
              &.special
                background: url('./special_1@2x.png')
                background-size: 100% 100%
              &.invoice
                background: url('./invoice_1@2x.png')
                background-size: 100% 100%
              &.guarantee
                background: url('./guarantee_1@2x.png')
                background-size: 100% 100%
            .detail-youhui-text
              vertical-align: middle
      .detail-gonggao
        .detail-gaoggao-name
          margin: 28px 36px
          position: relative
          display: flex
          .detail-gaoggao-hr
            width: 100%
            flex: 1
            height: 2px
            display: block
            top: 8px
            position: relative
            background: rgba(255, 255, 255, 0.2)
          .detail-gaoggao-title
            font-size: 16px
            font-weight: 700
            line-height: 16px
            padding: 0 12px
        .detail-gonggao-text
          text-align: left
          font-size: 12px
          margin: 28px 36px
          line-height: 24px
    .guanbi
      position: absolute
      bottom: 0
      width: 100%
      margin-bottom: 32px
      .guanbi-ioc
        display: block
        margin: 0 auto
        bottom: 0
        background: url('./guanbi.png')
        width: 32px
        height: 32px
        background-size: 100% 100%
</style>

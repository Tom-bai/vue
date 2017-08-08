<style lang="stylus" rel="stylesheet/stylus">
@import "../../assets/stylus/mixin.styl"
.recommend
  .box
    display: flex
    border-1px: #ccc
    padding: 10px
  .headerLogo
    flex: 0 0  40px
    >img
      border-radius: 50%
  .youMain
    flex: 1
    padding-left: 10px
    .youName
      font-size: 16px
      padding: 0px 10px 0px 0
      .sex
        width: 20px
        height: 20px
        display: inline-block
        background-size: 20px 20px
        background-repeat: no-repeat
        vertical-align: top
        &.nan
          bg-image('nan')
        &.nv
          bg-image('nv')
    .youText
      font-size:12px
      padding:5px 0 10px 0
      color: #999
    .blurRed
      >a
        display:block
      .blurImg
        width: 70%
</style>
<template>
  <div class="recommend">
    <div class="box" v-for="(item,index) in articleData">
      <div class="headerLogo"><img :src="item.avatar" alt="" width="40" /></div>
      <div class="youMain" v-for="pay in item.pay" >
          <div class="youName">{{item.username}} <i class="sex" :class="classMap[item.sex]"></i></div>
          <div class="youText">{{item.text}}</div>
          <div class="blurRed"  @click="selectFood(pay,$event)"><img :src="item.avatar" alt="" class="blurImg" /></div>
      </div>
    </div>
    <pay :pay="selectedFood" ref="pay"></pay>
  </div>
</template>

<script>
import pay from '../../components/pay/pay'
export default {
  data () {
    return {
      articleData: [],
      selectedFood: {}
    }
  },
  mounted () {
    this.fetchData()
  },
  created () {
    this.classMap = ['nan', 'nv']
  },
  computed: {},
  methods: {
    fetchData () {
      let _this = this
      _this.$http.get('static/data.json').then(function (res) {
        _this.articleData = res.data
        console.log(JSON.stringify(_this.articleData[0].pay[0].money))
      }).catch(function (err) {
        console.log(err)
      })
    },
    payshow () {
      console.log(this.$refs.pay)
      this.$refs.pay.show()
    },
    selectFood (pay, event) {
      console.log(this.$refs.pay)
      this.selectedFood = pay
      this.$refs.pay.show()
    }
  },
  components: {
    pay
  }
}
</script>

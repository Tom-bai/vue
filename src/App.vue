<template>
  <div id="app">
    <myHeader></myHeader>
    <div class="headbox">
      <div class="tab">
        <div class="tab-item">
          <router-link to="/Recommend" class="aBlock">商品</router-link>
        </div>
        <div class="tab-item">
          <router-link to="/pay" class="aBlock">评论</router-link>
        </div>
        <div class="tab-item">
          <router-link to="/hello" class="aBlock">商家</router-link>
        </div>
      </div>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
import myHeader from './components/header/header.vue'
export default {
  data () {
    return {
      seller: {}
    }
  },
  mounted () {
  },
  methods: {
    getDate () {
      this.$http.get('static/data/data.json').then((res) => {
        console.log(res.data)
        this.seller = res.data
      })
    }
  },
  components: {
    myHeader
  }
}

</script>
<style lang="stylus" rel="stylesheet/stylus">
.headbox
    width:100%
    border-bottom: solid 1px rgba(7,17,27,0.1)
  .tab
    display:flex
    width:100%
    height:40px
    line-height: 40px
    text-align: center
    .tab-item
      flex:1
      .aBlock
        display: block
        font-size: 14px
        font-weight: 200
        color: #000
      .router-link-active
        color:#f01414
        background:#fff
</style>


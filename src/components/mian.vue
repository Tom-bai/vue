<style scoped>
.ji{
  position: absolute;
  color:#999;
  padding:0 10px;
  top: 12px;
  left:40%;
  font-size: 12px;
  background-color: #f1f1f1;
}
.time-nav{
  font-size: 12px;
  text-align: left;
  padding:10px 0;
}
.time-nav span{
  font-weight: bold;
  padding:0 5px;
}
.ul ul{
    list-style: none;
    overflow: hidden;
}  
.ul ul li{
    width:30%;
    float: left;
    padding:4px;
}
.ul ul li img{
    width:100%;
}
.xiangce-text{
  text-align: left;
}
.xiangce-text h4{
  padding:10px 0;
}
.xiangce-ul{
  list-style: none;
  font-size: 16px;
  color:#999;
}
.xiangce-ul li{
  padding-bottom:5px;
}
.xiangce-ul li span{
  padding-left: 10px;
}
.cc{
  width:20px;
  color:#f18585;
  height:3px;
  border:3px #f18585;
  background-color:#f18585;
  margin-bottom: 10px;
}
.fenxiang{
  position: relative;
  padding:10px 0;
}
.fen1{
  position: absolute;
  right: 0;
  top: -8px;
  list-style: none;
}
.fen1 li{
  float: left;
  padding: 0 10px;
}
.fen1 li img{
  border-radius: 50%;
  border:solid 1px #f18585;
  padding:5px;
  background-color: #f1f1f1;
}
</style>
<template>
    <div>
      <hr />
      <span class="ji">我的作品集</span>
      <div id="zb-box">
        <div class="time-nav"><time>2017-03-15 09:34</time><span>未发布</span></div>
        <div class="ul">
          <ul>
              <li><img src="../assets/2.png" alt="" /></li>
              <li><img src="../assets/2.png" alt="" /></li>
              <li><img src="../assets/2.png" alt="" /></li>
          </ul>
        </div>
        <div class="xiangce-text">
          <h4>我的私密相册~</h4>
          <hr class="cc" />
          <ul class="xiangce-ul">
            <li>共收到打赏<span>￥0</span></li>
            <li>被打赏次数<span>0</span></li>
            <li>总浏览次数<span>0</span></li>
          </ul>
          <div class="fenxiang">
            <hr />
            <ul class="fen1">
              <li><img src="../assets/laji.png" width="24px"  alt="" /></li>
              <li><img src="../assets/xiugai.png" width="24px"  alt="" /></li>
              <li><img src="../assets/fenxiang.png" width="24px"  alt="" /></li>
            </ul>
          </div>
        </div>
      </div>
      <div id="zb-box">
        <div class="time-nav"><time>2017-03-15 09:34</time><span>未发布</span></div>
        <div class="ul">
          <ul>
              <li><img src="../assets/2.png" alt="" /></li>
              <li><img src="../assets/2.png" alt="" /></li>
              <li><img src="../assets/2.png" alt="" /></li>
          </ul>
        </div>
        <div class="xiangce-text">
          <h4>我的私密相册~</h4>
          <hr class="cc" />
          <ul class="xiangce-ul">
            <li>共收到打赏<span>￥0</span></li>
            <li>被打赏次数<span>0</span></li>
            <li>总浏览次数<span>0</span></li>
          </ul>
          <div class="fenxiang">
            <hr />
            <ul class="fen1">
              <li><img src="../assets/laji.png" width="24px"  alt="" /></li>
              <li><img src="../assets/xiugai.png" width="24px"  alt="" /></li>
              <li><img src="../assets/fenxiang.png" width="24px"  alt="" /></li>
            </ul>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
export default {
  data () {
    return {}
  },
  computed: {}
}
</script>

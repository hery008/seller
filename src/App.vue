<template>
  <div id="app">
      <v-header :seller="seller"></v-header>
    <div class="tab border-1px">
      <router-link class="tab-item" to="/goods">
        <div class="tab-item currentSpan">商品</div>
      </router-link>
      <router-link class="tab-item" to="/ratings">
        <div class="tab-item">评论</div>
      </router-link>
      <router-link class="tab-item" to="/seller">
        <div class="tab-item">商家</div>
      </router-link>
    </div>
    <router-view :seller="seller"></router-view>
    
  </div>
</template>

<script>
import header from './components/header/header'
import axios from 'axios'
import $ from 'jquery'

export default {
  name: 'App',
  components:{
    'v-header':header
  },
  data() {
    return {
        seller:{}
    }
  },
  created(){
      axios.get('../static/data.json')
      .then(res=>{
        // console.log(res.data.seller)
        this.seller = res.data.seller
      })
      .catch(err=>{
        console.log(err)
      })
  },
  mounted(){
    $(".tab-item").click(function(){
      $(this).addClass("currentSpan").siblings().children().removeClass("currentSpan")
    })
  },
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
@import './common/stylus/mixin'
  #app
    .tab
      display:flex;
      width :100%
      height 40px
      line-height :40px;
      // border-bottom:1px solid rgba(7,17,27,0.1)
      border-1px(rgba(7,17,27,0.1))
      .tab-item
        flex:1
        text-align:center

.currentSpan
  color:red
</style>

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
    <router-view></router-view>
    
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
        seller:''
    }
  },
  created(){
      axios.get('../static/data.json')
      .then(res=>{
        console.log(res.data.seller)
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
  methods:{
    getData(){

    // $.ajax({
    //       type: 'GET',
    //       url:'https://api.nal.usda.gov/ndb/list?format=json&lt=n&sort=n&api_key=xmvRjoCM6BNaK0mSsqgRnXTeP06lgVdpC0ypsyy7',
    //       dataType:'jsonp',
    //       jsonp:"callback",
    //       contentType:'application/json',
    //       success: function(data) {
    //         // JSON.stringify(data);
    //         // var data=data.query.results.json.result.data;
    //         console.log(JSON.stringify(data));             
    //       },
    //       error: function(error) {
    //         console.log(error);
    //       }
    //     });
      // this.$jsonp('https://api.nal.usda.gov/ndb/list?format=json&lt=n&sort=n&api_key=xmvRjoCM6BNaK0mSsqgRnXTeP06lgVdpC0ypsyy7').then(res => {
      //   console.log(JSON.stringify(res))
      // }).catch(err => {
      //   console.log(err)
      // })
      // axios.get('/api/?format=json&lt=f&sort=n&api_key=xmvRjoCM6BNaK0mSsqgRnXTeP06lgVdpC0ypsyy7&max=10')
      // .then(res=>{
      //   console.log(res)
      // })
      // .catch(err=>{
      //   console.log(err)
      // })
      // let obj = {
      //         'format':'json',
      //         'lt':'n',
      //         'max':10,
      //         'api_key':'xmvRjoCM6BNaK0mSsqgRnXTeP06lgVdpC0ypsyy7',
      //         'sort':'n'
      //     }
      //     this.$jsonp('https://api.nal.usda.gov/ndb/list/', obj).then(res => {
      //     　　console.log(res.item)
      //     }).catch(err => {
      //     　　console.log(err)
      //     })


      // this.$jsonp('https://api.nal.usda.gov/ndb/list', { max: 20,'api_key':'xmvRjoCM6BNaK0mSsqgRnXTeP06lgVdpC0ypsyy7', 'lt':'n','sort':'n'}).then(json => {
      //   console.log(json)
      // }).catch(err => {
      //   console.log(err)
        
      // })    
    }
  }
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

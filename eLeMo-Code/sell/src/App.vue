<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
<!--        <router-link  v-link="{path:'/goods'}">商品</router-link >-->
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评论</router-link>
        <!--<a v-link="{path:'/goods'}">评论</a>-->
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
        <!--<a v-link="{path:'/goods'}">商家</a>-->
      </div>
    </div>
    <router-view　:seller="seller"></router-view>
  </div>
</template>

<script type="text/ecmascript-6">
import header from './components/header/header.vue';
const ERR_OK=0;
  export default{
      data: function () {
        return{
          seller:{

          }
        }
      },
      created:function(){
        this.$http.get('/api/seller').then((response)=>{
          console.log(response)
               response=response.body;
          if(response.errno===ERR_OK){
            this.seller=response.data;
            console.log(this.seller)
          }

        })
      },
      components:{
        'v-header':header
      }
    };
</script>

<style>
  @import "./common/stylus/icon.css";
/*  @import "./common/stylus/minix.less";*/
#app .tab {
  display: flex;
  width: 100%;
  height: 40px;
  line-height: 40px;
/*border-1px(rgba(7,17,27,0.1));*/
  border-bottom: 1px solid rgba(7,17,27,0.1);
}
#app .tab .tab-item{
  flex: 1;
  text-align: center;
}
#app .tab .tab-item>a{
  display: block;
  text-decoration: none;
  font-size: 14px;
  color:rgb(77,85,93)
}
#app .tab .tab-item .active{
  color:rgb(240,20,20)
}

</style>

<template>
  <div id="detail">
    <detail-nav-bar></detail-nav-bar>
    <detail-swiper :top-images="topImages"></detail-swiper>
    <detail-base-info :goods="goods"></detail-base-info>
    <detail-shop-info :shop="shop"></detail-shop-info>
    <detail-bottom-bar @addCart="addToCart"></detail-bottom-bar>
    <back-top @click="backClick"></back-top>
    
  </div>
</template>

<script>
import DetailNavBar from './childComps/DetailNavBar.vue'
import {getDetail,Goods,Shop} from '../../network/detail'
import DetailSwiper from './childComps/DetailSwiper.vue'
import DetailBaseInfo from './childComps/DetailBaseInfo.vue'
import DetailShopInfo from './childComps/DetailShopInfo.vue'
import DetailBottomBar from './childComps/DetailBottomBar.vue'
import BackTop from 'components/content/backtop/BackTop.vue'


export default {
  name:'Detail',
  components:{
    DetailNavBar,
    DetailSwiper,
    DetailBaseInfo,
    DetailShopInfo,
    DetailBottomBar,
    BackTop
  },
  created(){
    this.iid=this.$route.params.iid

    getDetail(this.iid).then(res=>{
      const data=res.result;
      //获取顶部图片的轮播数据
      this.topImages=res.result.itemInfo.topImages
      //获取商品信息
    this.goods=new Goods(data.itemInfo,data.columns,data.shopInfo.services)
    //创建店铺信息的对象
    this.shop=new Shop(data.shopInfo)
    })
    
  },
  data(){
    return{
      iid:null,
      topImages:[],
      goods:{},
      shop:{}
    }
  },
  methods:{
    backClick(){
    window.scrollTo(0,0)
   },
   addToCart(){
     //获取购物车需要展示的信息
     const product={}
     product.image=this.topImages[0];
     product.title=this.goods.title;
     product.desc=this.goods.desc;
     product.price=this.goods.realPrice;
     product.iid=this.iid;
     //将商品添加到购物车
    this.$store.dispatch('addCart',product)
   }
  }
}
</script>

<style>
  #detail{
    position: relative;
    z-index: 9;
    background-color: #fff;
  }
</style>
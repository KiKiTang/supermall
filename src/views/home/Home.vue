<template>
  <div id="home">
    <nav-bar class="home-nav">
      <template v-slot:center><div>购物街</div></template>
    </nav-bar>
    <home-swiper :banners="banners"/>
    <home-recommend-view :recommends="recommends"/>
    <feature-view></feature-view>
    <tab-control :class="tab-control" :titles="['流行','新款','精选']"
    @tabClick="tabClick"></tab-control>
    <back-top @click="backClick"></back-top>
    <goods-list :goods="goods[currentType].list"></goods-list>
    
  </div>
</template>

<script>
import NavBar from 'components/common/navbar/NavBar.vue'
import {getHomeMultidata,getHomeGoods} from 'network/home.js'
import HomeSwiper from './childComps/HomeSwiper.vue'
import HomeRecommendView from './childComps/HomeRecommendView.vue'
import FeatureView from './childComps/FeatureView.vue'
import TabControl from 'components/content/tabControl/TabControl.vue'
import GoodsList from 'components/content/goods/GoodsList.vue'
import BackTop from 'components/content/backtop/BackTop.vue'

export default {
  name:"Home",
  components:{
    NavBar,
    HomeSwiper,
    HomeRecommendView,
    FeatureView,
    TabControl,
    GoodsList,
    BackTop
  },
  data(){
    return{
      banners:[],
      recommends:[],
      goods:{
        'pop':{page:0,list:[]},
        'new':{page:0,list:[]},
        'sell':{page:0,list:[]},
      },
      currentType:'pop'
    }
  },
  created(){
    //请求多个数据
    this.getHomeMultidata()
    //请求商品数据
    this.getHomeGoods('pop')
    this.getHomeGoods('new')
    this.getHomeGoods('sell')
  },
  methods:{
    tabClick(index){
      switch(index){
        case 0:
          this.currentType='pop'
          break;
        case 1:
          this.currentType='new'
          break;
        case 2:
          this.currentType='sell'
          break;
      }
    },
    getHomeMultidata(){
    getHomeMultidata().then(res => {
    this.banners=res.data.banner.list;
    this.recommends=res.data.recommend.list;
    })
   },
   backClick(){
    window.scrollTo(0,0)
   },
    getHomeGoods(type){
      const page=this.goods[type].page+1
      getHomeGoods(type,page).then(res=>{
        //将第1页的数据传给goods的第0页
          //this.goods[type].list.push(...res.data.list)
          for(let n of res.data.list){
            this.goods[type].list.push(n)
          }
        //goods翻到第1页
        this.goods[type].page+=1
    })
    }
  }
}
</script>

<style>
#home{
  padding-top: 44px;
}
  .home-nav{
    background-color: var(--color-tint);
    color: white;

    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    z-index: 9;
  }
  .tab-control{
    position: sticky;
    top:44px;
    z-index: 9;
  }
</style>
<template>
   <Tabbar>
      <tab-bar-item path="/home" activeColor="red">
        <template v-slot:item-icon><img src="~assets/img/首页.png"></template>
        <template v-slot:item-icon-active><img src="~assets/img/首页2.png"></template>
        <template v-slot:item-text><div>首页</div></template>
      </tab-bar-item>
      <tab-bar-item path="/category" activeColor="red">
        <template v-slot:item-icon><img src="~assets/img/瀑布流.png"></template>
        <template v-slot:item-icon-active><img src="~assets/img/瀑布流2.png"></template>
        <template v-slot:item-text><div>分类</div></template>
      </tab-bar-item>
      <tab-bar-item path="/cart" activeColor="red">
        <template v-slot:item-icon><img src="~assets/img/05采购-线性.png"></template>
        <template v-slot:item-icon-active><img src="~assets/img/05采购.png"></template>
        <template v-slot:item-text><div>购物车</div></template>
      </tab-bar-item>
      <tab-bar-item path="/profile" activeColor="red">
        <template v-slot:item-icon><img src="~assets/img/224用户-线性.png"></template>
        <template v-slot:item-icon-active><img src="~assets/img/224用户.png"></template>
        <template v-slot:item-text><div>我的</div></template>
      </tab-bar-item>
    </Tabbar>
</template>

<script>
import Tabbar from 'components/common/tabbar/tabbar.vue'
import TabBarItem from 'components/common/tabbar/TabBarItem.vue'

export default {

  name:"MainTabBar",
  components:{
    Tabbar,
    TabBarItem
  }
}
</script>

<style>

</style>
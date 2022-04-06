<template>
  <div class="cart">
    <nav-bar class="nav-bar">
      <template v-slot:center><div>购物车({{cartLength}})</div></template>
    </nav-bar>
    <!--商品的列表-->
    <cart-list></cart-list>
    <cart-bottom-bar></cart-bottom-bar>
  </div>
</template>

<script>
import NavBar from '../../components/common/navbar/NavBar.vue'
import {mapGetters} from 'vuex'
import CartList from './childComps/CartList.vue'
import CartBottomBar from './childComps/CartBottomBar.vue'

export default {
  components: { NavBar, CartList,CartBottomBar },
  name:'Cart',
  computed:{
    ...mapGetters(['cartLength']),
  }
}
</script>

<style>
.nav-bar{
  background-color: var(--color-tint);
  color: #fff;
  font-weight: 700;
  position: sticky;
}
.cart{
  height: 100vh;
}
</style>
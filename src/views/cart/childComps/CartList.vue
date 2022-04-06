<template>
  <div class="cart-list">
    <cart-list-item v-for="(item,index) in cartList" :key="index" :item-info="item"></cart-list-item>
  </div>
</template>

<script>
import {mapGetters} from 'vuex'
import CartListItem from './CartListItem.vue'

export default {
  components: { CartListItem },
  name:'CartList',
  computed:{
    ...mapGetters(['cartList']),
  }
}
</script>

<style>
.cart-list{
  height: calc(100% - 44px - 49px - 40px);
}
</style>
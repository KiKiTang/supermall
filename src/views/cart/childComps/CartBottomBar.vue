<template>
  <div class="bottom-bar-cart">
    <div class="check-content">
  <check-bottom class="check-button" :is-checked="isSelectAll"
  @click="checkClick"></check-bottom>
  <span>全选</span>
  </div>
  <div class="price">
    合计：{{totalPrice}}
  </div>
  <div class="calculate">去结算({{checkLength}})</div>
  </div>
  
</template>

<script>
import CheckBottom from '../../../components/content/checkButtom/CheckBottom.vue'

export default {
  components: { CheckBottom },
  name:'CartBottomBar',
  computed:{
    totalPrice(){
       return '￥'+this.$store.state.cartList.filter(item=>{
         return item.checked
       }).reduce((preValue,item)=>{
         return item.price*item.count+preValue
       },0).toFixed(2)
    },
    checkLength(){
      return this.$store.state.cartList.filter(item=>{return item.checked}).length;
    },
    isSelectAll(){
      //this.$store.state.cartList.filter(item=>!item.checked).length
      if(this.$store.state.cartList.length===0)return false
      return !this.$store.state.cartList.find(item=>!item.checked)
    }
   
  },
  methods:{
    checkClick(){
      if(this.isSelectAll){
        this.$store.state.cartList.forEach(item=>item.checked=false)
      }else{
        this.$store.state.cartList.forEach(item=>item.checked=true)
      }
    }
  }
}
</script>

<style>
.bottom-bar-cart{
  background-color:#fff;
  height: 40px;
  width: 100%;
  z-index: 10;
  position: fixed;
  left: 0px;
  right: 0px;
  bottom: 49px;
  display: flex;
}
.check-content{
  margin-top: 8px;
  display: flex;
  align-items: center;
  margin-left: 5px;
  font-size: 16px;
}
.check-button{
  width: 24px;
  height: 24px;
  line-height: 20px;
}
.price{
  margin-left: 20px;
  margin-top: 15px;
  flex: 1;
}
.calculate{
  width: 90px;
  background:red;
  text-align: center;
  line-height: 30px;
}
</style>
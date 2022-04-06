<template>
  <div class="check-buttom" :class="{check:isChecked}">
    <img src="~assets/img/check-item.png" alt="">
  </div>
</template>

<script>
export default {
name:'CheckBottom',
props:{
  isChecked:{
    type:Boolean,
    default:true
  }
}
}
</script>

<style>
.check-buttom{
width: 20px;
height: 20px;
border: 2px solid #aaa;
}
.check-buttom img{
  width: 20px;
  height: 20px;
}
.check{
  border-color:red;
  background-color: red;
}
</style>
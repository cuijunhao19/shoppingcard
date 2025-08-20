<script>
// 引入组件
import ShoppingCard from './components/ShoppingCard.vue'
export default {
  name: 'app',
  components: {
    ShoppingCard
  }
}
</script>

<template>
  <div class="box">
    <div class="title">
      <span class="check">选择</span>
      <span class="name">商品信息</span>
      <span class="unitPrize">商品单价</span>
      <span class="num">商品数量</span>
      <span class="unitTotalPrize">商品金额</span>
      <span class="operation">操作</span>
    </div>
    <ShoppingCard />
  </div>
</template>

<style lang="scss">
@import './assets/css/style.css';
</style>

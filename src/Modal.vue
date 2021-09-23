<template>
  <div class="black-bg" v-if="modalStat">
    <div class="white-bg">
      <img :src="products[clickStat].image" style="width:100%">
      <h4>{{products[clickStat].title}}</h4>
      <p>{{products[clickStat].content}}</p>
      <p>{{products[clickStat].price}} 만원</p>
      <button v-on:click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
    name:"Modal",
    props:{
        products:Array,
        clickStat:Number,
        modalStat:Boolean,
    },
}
</script>

<style>
.black-bg{
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed; /*뷰포트기준으로 위치절대고정(마우스휠에도영향안받음)*/
  top:0;
  padding: 20px;
}
.white-bg{
  width: 70%;
  background: white;
  border-radius: 8px;
  padding: 20px;
  margin: 0 auto;
}
</style>
<template>
  <div class="black-bg" v-if="modalStat">
    <div class="white-bg">
      <img :src="products[clickStat].image" style="width:100%">
      <h4>{{products[clickStat].title}}</h4>
      <p>{{products[clickStat].content}}</p>
      <input type="text" :value="month" @input="month=$event.target.value"><!--e.target.value //js문법-->
      <!--<input type="text" v-model.number="month">  두번째 input방법 -->
      <p>{{month}}개월 선택함 : {{products[clickStat].price * month}} 만원</p>
      <button v-on:click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
    name:"Modal",
    data() {
      return {
        month:1
      }
    },
    watch:{
      //month가 변경될때마다 실행
      month(after,before){
        //isNaN() 문자열 true , 숫자 false
        if(isNaN(after)){
          alert("숫자를 입력해주세요")
          this.month=1;
          console.log(this.month)
        }
        if (after>12) {
          this.month=before
          alert("12개월까지 가능합니다")
        }
      },
    },
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
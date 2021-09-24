<template>
  <!-- 매뉴 -->
  <div class="menu">
    <a v-for="(elem,idx) in menus" :key="idx" href="">{{elem}}</a>
  </div>
  <button @click="sortPrice">가격순정렬</button>
  <button @click="backPrice">되돌리기</button>
  <!-- 디스카운트 -->
  <transition name="swing">
    <Discount v-if="discountState" :discountRate="discountRate"/>
  </transition>
  <!-- 모달 -->
  <div class="start" :class="{end:modalStat}">
      <Modal @closeModal="modalStat=false;" :products="products" :clickStat="clickStat" :modalStat="modalStat"/>
  </div>
  <!-- 상품정보 리스트 -->
  <Card @openModal="modalStat=true;clickStat=$event"  :product="products[idx]" v-for="(elem,idx) in products" :key="elem.id" />
</template>

<script>
import testData from './assets/testRoomData.js'
import Discount from './Discount.vue'
import Modal from './Modal.vue'
import Card from './Card.vue'

export default {
  name: 'App',
  data() {
    return {
      clickStat:0,
      modalStat:false,
      reportCnt:[0,0,0],
      menus:["Home","Shop","About"],
      productsOrigin:[...testData],
      products:testData,
      styleTest:"color:darkslateblue",
      discountState:true,
      discountRate:10
    }
  },
  methods: {
    report(idx){
      this.reportCnt[idx]+=1
    },
    mouseOverButton(e) {
      console.log(e)
    },
    closeModal(){
      this.modalStat=false
    },
    sortPrice(){
      this.products.sort((a,b)=>{
        return a.price-b.price
      })
    },
    backPrice(){
      this.products=[...this.productsOrigin]
    }
  },
  created(){
    setInterval(() => {
      this.discountRate-=1
    }, 1000);
  },
  mounted(){
    // 애로우펑션을 사용하면 this를 사용해서 외부블록의 변수를 가져올수있다.
    setTimeout(()=>{
      this.discountState=false;
    }, 10000);
  },
  components: {
    Discount:Discount,
    Modal:Modal,
    Card:Card
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.menu{
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a{
  color: white;
  padding: 10px;
}
body{
  margin: 0;
}
div{
  box-sizing: border-box;/*태두리를 포함한 크기를 지정하게 됨*/
}
/* 애니메이션 */
.start{
  opacity: 0;
  transition: all 1s;
}
.end{
  opacity: 1;
}
/* 시작~종료 무지성 뷰 애니메이션 */
.swing-enter-from{opacity: 1;}
.swing-enter-active{transition: all 1s ease;}/*1초동안 일정한속도로 */
.swing-enter-to{opacity:0}
</style>

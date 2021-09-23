<template>
  <!-- 매뉴 -->
  <div class="menu">
    <a v-for="(elem,idx) in menus" :key="idx" href="">{{elem}}</a>
  </div>
  <!-- 디스카운트 -->
  <Discount/>
  <!-- 모달 -->
  <Modal @closeModal="modalStat=false;" :products="products" :clickStat="clickStat" :modalStat="modalStat"/>
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
      products:testData,
      styleTest:"color:darkslateblue"
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
    }
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
</style>

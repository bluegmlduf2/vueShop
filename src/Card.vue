<template>
    <div>
      <img class="room-img" :src="product.image" alt="" @mouseover="addOpacity" @mouseleave="removeOpacity">
      <h4 v-on:click="openModal" :style="styleTest">{{product.title}}</h4><!--부모에게보낼떄 customEvent-->
      <p>{{product.price}} 만원</p>
      <!-- <button @mouseover="mouseOverButton($event)" v-on:click="report(idx)">허위매물신고</button>  -->
      <!-- <span>신고수 : {{reportCnt[idx]}}</span> -->
    </div>
</template>

<script>
export default {
    name:"Card",
    props:{
        product:Array
    },
    methods: {
      openModal(){
        this.$emit('openModal',this.product.id)
//modalStat=true;clickStat=idx
      },
      addOpacity(e){
        e.target.style.opacity=0.5;
        e.target.parentElement.children[1].style.color="darkslateblue";
      },
      removeOpacity(e){
        e.target.style.opacity=1;
        e.target.parentElement.children[1].style.color="#2c3e50";
      }
    },
}
</script>

<style>
.room-img{
  width: 100%;
  margin-top: 40px;
}
</style>
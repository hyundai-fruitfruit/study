/* eslint-disable */
<template>

  <transition name="fade">
    <ProductModal @closeModal="모달창상태=false;" :원룸들="원룸들" :누른거="누른거" :모달창상태="모달창상태"/>
  </transition>>


  <div class="menu">
    <a v-for="작명 in 메뉴들" :key="작명">{{ 작명 }}</a>
  </div>

  <DiscountBanner v-if="showDiscount == true" :amount="amount"/>

 
  <button @click="sortBack">되돌리기</button>
  <button @click="priceSort">가격순정렬</button>
  <button @click="priceSortReverse">가격역순정렬</button>
  <button @click="priceSortName">문자정렬</button>

  <ProductCard @openModal="모달창상태=true; 누른거 = $event" :원룸="원룸들[i]" v-for="(a,i) in 원룸들" :key="i"   />


</template>

<script>

import data from './assets/oneroom.js';
import DiscountBanner from './components/DiscountBanner.vue';
import ProductModal from './components/ProductModal.vue';
import ProductCard from './components/ProductCard.vue';


export default {
  name: 'App',
  data(){
    return{
      showDiscount : true,
      amount : 30,
      원룸들오리지널 : [...data],
      누른거 : 0,
      원룸들 : [...data],
      모달창상태 : false,
      메뉴들 : ['Home', 'Shop', 'About'],
      products : ['역삼동원룸', '천호동원룸', '마포구원룸' ],
      prices : ['50만원', '가격은 아무거나'],
      신고수 : [0,0,0],
    }
  },

  methods : {
    increase(i) {
      this.신고수[i]++;
    },
    priceSort() {
      this.원룸들.sort(function(a,b){
        return a.price - b.price
      });
    },
    priceSortReverse() {
      this.원룸들.sort(function(a,b){
        return b.price - a.price
      });
    },
    priceSortName() {
      this.원룸들.sort(function(a, b) {
        return a.title.localeCompare(b.title);
      });
    },
    sortBack() {
      this.원룸들 = [...this.원룸들오리지널];
    },
  },

  mounted() {
    setTimeout(() => {
      this.amount--;
    },1000);
  },


  components: {
    DiscountBanner : DiscountBanner,
    ProductModal : ProductModal,
    ProductCard : ProductCard,
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
.room-img{
  width: 100%;
  margin-top: 40px;
}
body{
  margin: 0;
}
div {
  box-sizing: border-box;
}
.black-bg {
  width: 100%; height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
}
.white-bg{
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
}
.fade-enter-from {
  transform: translateY(-1000px);
}
.fade-enter-active {
  transition: all 1s;
}
.fade-enter-to {
  transform: translateY(0);
}

.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 1s;
}
.fade-leave-to {
  opacity: 0;
}

</style>

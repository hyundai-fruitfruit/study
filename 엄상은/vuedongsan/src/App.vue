<template>

  <Transition name="fade">
    <Modal @closeModal="is_modal_open=false" :oneroom="oneroom" :id="id" :is_modal_open="is_modal_open"/>
  </Transition>

  <div class="menu">
    <a v-for="a in menu" :key="a"> {{ a }} </a>
  </div>

  <Discount v-if="showDiscount==true" />

  <button @click="titleSort()">가나다순</button>
  <button @click="priceSort()">가격순정렬버튼</button>
  <button @click="priceReverseSort()">가격역순정렬버튼</button>
  <button @click="sortBack()">되돌리기</button>

  <Card @openModal="is_modal_open=true; id=$event" v-for="(x, i) in oneroom" :key="i" :room="oneroom[i]"/>

</template>

<script>

import data from './data/oneroom'
import Discount from './Discount.vue'
import Modal from './Modal.vue'
import Card from './Card.vue'


export default {
  name: 'App',
  data() {
    return {
      showDiscount: true,
      is_modal_open: false,
      menu: ['Home', 'Shop', 'About'],
      counts: [0, 0, 0, 0, 0, 0],
      oneroom: data,
      oneroom_orig: [...data],
      id: null,
    }
  },
  components: {
    Discount: Discount,
    Modal: Modal,
    Card: Card,
  },
  mounted() {
    setTimeout(() => {
      this.showDiscount = false;
    }, 2000);
  },
  methods: {
    increase(x) {
      this.counts[x]++;
    },
    titleSort() {
      this.oneroom.sort(function(a, b) {
        if(a.title.toLowerCase() > b.title.toLowerCase())
          return 1;
        else if(a.title.toLowerCase() < b.title.toLowerCase())
          return -1;
        else
          return 0;
      })
    },
    priceSort() {
      this.oneroom.sort(function(a, b) {
        return a.price - b.price;
      })
    },
    priceReverseSort() {
      this.oneroom.sort(function(a, b) {
        return b.price - a.price;
      })
    },
    sortBack() {
      this.oneroom = [...this.oneroom_orig];
    }
  }
}
</script>

<style>
.fade-enter-from {
  transform: translateY(-1000px);
}
.fade-enter-active {
  transition: all 1s;
}
.fade-enter-to {
  transform: translateY(0px);
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

body {
  margin: 0
}

div {
  box-sizing: border-box;
}

.discount {
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}

.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}

.white-bg {
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}

.room-img {
  width: 50%;
  margin-top: 40px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  margin: 10px;
}
</style>

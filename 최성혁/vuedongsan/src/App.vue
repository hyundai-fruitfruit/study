<template>
  <div>
    <div class="menu">
      <a v-for="(a, i) in 메뉴들" :key="i">{{ a }}{{ i }}</a>
    </div>
    <Modal @closeModal="모달창열렸니 = false;" :원룸들="원룸들" :누른거="누른거" :모달창열렸니="모달창열렸니"/>
    
    <Card @openModal="모달창열렸니 = true; 누른거 = $event"
          :원룸="원룸들[idx]"
          v-for="(val, idx) in 원룸들"
          :key="val"
    />
  </div>
</template>


<script>
import data from './assets/oneroom.js';
import Modal from './Modal.vue';
import Card from './Card.vue';

export default {
  name: 'App',
  data(){
    return {
      누른거 : 0,
      원룸들 : data,
      모달창열렸니 : false,     //모달창의 현재 상태
      신고수 : [0,0,0],
      메뉴들 : ['Home','Products','About'],
      products : ['역삼동원룸','천호동원룸','서초동원룸']
    }
  },
  methods : {
    increase(){
    this.신고수[0] += 1;
    },
    increase_one(){
    this.신고수[1] += 1;
    },
    increase_two(){
    this.신고수[2] += 1;
    }
  },
  components: {
    Modal : Modal,
    Card: Card
  }
}
</script>




<style>
body{
  margin: 0;
}
div {
  box-sizing: border-box;
}
.discount{
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}
.black-bg{
  width: 100%; height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
}
.white-bg{
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
}

.room-img{
  width: 100%;
  margin-top: 40px;
}
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

</style>

<template>
    <div>
      <div>
        <a v-for="(menu, i) in menus" :key="i"> {{ menu }}</a>
      </div>

      <DiscountComponent/>
      <ModalComponent @closeModal="isModalOpen = false" :oneroom="oneroom" :isButton="isButton" :isModalOpen="isModalOpen"/>
      <CardComponent @openModal="isModalOpen = true; isButton = $event" :oneroom="oneroom" :isButton="isButton" :isModalOpen="isModalOpen"/>

      <!-- 상품 리스트 -->
      <!-- <div v-for="(a, i) in oneroom" :key="i">
        <img :src="oneroom[i].image" class="room-img">
        <h4 @click="isModalOpen = true; isButton = i">{{oneroom[i].title}}</h4>
        <p>{{oneroom[i].price}}</p>
      </div> -->

      <!-- 모달창 만들기 -->
      <!-- 2. 데이터 상태에 따라 HTML UI을 보여줄지 말지를 Vue문법으로 작성함  -->
     <!-- <div @click="isModalOpen = true" v-if="isModalOpen == false" >모달창 보기 버튼</div> -->
     <!-- <div class="black-bg" v-if="isModalOpen == true"> 
        <div class="white-bg">
          <h4>{{ oneroom[isButton].title }}</h4>
          <p>{{ oneroom[isButton].content }}</p>
          <p>{{ oneroom[isButton].price }}</p>
          <button @click="isModalOpen = false">닫기</button>
        </div>
      </div> -->

    </div>
</template>

<script>
import oneroomData from './assets/oneroom';
import DiscountComponent from './Discount.vue';
import ModalComponent from './Modal.vue';
import CardComponent from './Card.vue';

export default {
  name: 'App',
  data() {
    return {
      oneroom : oneroomData,
      isModalOpen : false, // 1. 현재 모달창의 상태를 데이터로 저장해둡니다.
      menus : ['메뉴1', '메뉴2', '메뉴3'],
      products : ['원룸', '투룸', '쓰리룸'],
      warnCnt : 0,
      isButton : 0,
    

    }
  },
  methods : { // 메소드 추가
    increase() {
      this.warnCnt += 1
    }
  },
  components: {
    DiscountComponent,
    ModalComponent,
    CardComponent,
  }
}
</script>

<style>
body {
  margin : 0;
}
div {
  box-sizing: border-box;
}
.black-bg {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
}

.white-bg {
  width: 80%; /* Adjust the width as needed */
  max-width: 600px; /* Set a maximum width if desired */
  background: white;
  border-radius: 8px;
  padding: 20px;
}
</style>
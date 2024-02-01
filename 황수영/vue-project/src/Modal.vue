<template>
    
    <div class="black-bg" v-if="isModalOpen == true"> 
        <div class="white-bg">
          <h4>{{ oneroom[isButton].title }}</h4>
          <p>{{ oneroom[isButton].content }}</p>
          <!-- 사용자 입력 받는 방식들 -->
          <input @input="month = $event.target.value">
          <!-- 기본은 문자이기에 숫자형으로 지정 -->
          <!-- <input v-model.number="month"> 
          <textarea v-model="month"></textarea>
          <select v-model="month"></select> -->

          <p> {{month}} 개월 선택함 : {{ oneroom[isButton].price * month }}</p>

          <!-- props에서는 데이터 변경 불가 -->
          <button @click="$emit('closeModal')">닫기</button>
        </div>
    </div>

</template>

<script>
export default {
    name : 'ModalComponent',
    data() {
      return {
        month : 1,
        date : 123
      }
    },
    watch : {
      month(a) {
        if (isNaN(a) == true){
          alert('숫자 입력');
        }
        if (a >= 13){
          alert('12이하로 입력해야 함');
        }
      }
    },
    props : {
      oneroom : Array,
      isButton : Number,
      isModalOpen : Boolean
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
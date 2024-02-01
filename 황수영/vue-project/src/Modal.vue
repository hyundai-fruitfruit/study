<template>
    
    <div class="black-bg" v-if="isModalOpen == true"> 
        <div class="white-bg">
          <h4>{{ oneroom[isButton].title }}</h4>
          <p>{{ oneroom[isButton].content }}</p>
          <p>{{ oneroom[isButton].price }}</p>
          <!-- props에서는 데이터 변경 불가 -->
          <button @click="$emit('closeModal')">닫기</button>
        </div>
      </div>
</template>

<script>
export default {
    name : 'ModalComponent',
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
<template>
  
  <div class = "black-bg" v-if="모달창열렸니 == true">
    <div class="white-bg">
      <img :src="원룸들[누른거].image" class="room-img">
      <h4>{{원룸들[누른거].title}}</h4>
      <p>{{원룸들[누른거].content}}</p>
      <input v-model="month"> 
      <p> {{month}}개월 선택함 : {{원룸들[누른거].price * month}}원</p>
      <button @click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Modal',
  data(){
    return{
      month : 1,
    }
  },
  watch : {
    month(a){
      if (isNaN(a) == true){
        alert("문자입력하지마라")
        this.month = 1
      }
    },
  },
  updated(){
    if(this.month == 2){
      alert("2는안된다고 말했을텐데")
      this.month = 3
    }
  },
  props: {
    원룸들 : Object,
    누른거 : Number,
    모달창열렸니 : Boolean,
  }
}
</script>

<style>

</style>
/* eslint-disable */
<template>
    <div class="black-bg" v-if="모달창상태 == true">
        <div class="white-bg">
        <img :src="원룸들[누른거].image" class="room-img">
        <h4>{{원룸들[누른거].title}}</h4>
        <p>{{원룸들[누른거].content}}</p>
        <input v-model="month">
        <p> {{ month }}개월 선택함 : {{원룸들[누른거].price * month}}원</p>
        <button @click="$emit('closeModal')">닫기</button>
        </div>
  </div>
  
</template>

<script>

export default {
    name : "ProductModal",
    data(){
        return {
            month : 1,
        }
    },
    watch : {
        month(a) {
            if (isNaN(a) == true) {
                alert('숫자를 입력해주세요')
                this.month = 1;
            }
        }
    },
    props : {
        원룸들 : Array,
        누른거 : Number,
        모달창상태 : Boolean,
    },

    beforeUpdate() {
        if(this.month == 2) {
        alert('최소 3개월입니다.')
        }
    },
}
</script>

<style>

</style>
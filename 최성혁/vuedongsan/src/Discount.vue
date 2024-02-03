<template>
   <div class = "discount">
    <h4>지금 결제하면 {{퍼센트}}% 할인</h4>
  </div>
</template>

<script>
export default {
  name: 'Discount',
  data(){
    return{
      퍼센트 : 30,
      interval : null,
      돌리도퍼센트 : 30,
    }
  },
  mounted(){
  setInterval(() => { //1초마다 내부 코드 실행
    this.퍼센트 -= 1
    if (this.퍼센트 === 0) {
        this.퍼센트 = this.돌리도퍼센트; // 퍼센트가 0이 되면 setInterval을 중지합니다.
      }
  },1000);
  },
}
</script>

<style>

</style>
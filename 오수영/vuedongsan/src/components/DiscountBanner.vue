/* eslint-disable */
<template>
    <div class="DiscountBanner">
        <h4>지금 결제하면 {{ amount  }}% 할인</h4>
    </div>
</template>

<script>
export default {
    name: 'DiscountBanner',
    props : {
        amount : Int16Array,
    },

}
</script>

<style>
.DiscountBanner {
  background: white;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}

</style>
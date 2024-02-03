<template>
  
  <div>
    <h4>상세페이지</h4>
    <h5>{{ posts[$route.params.id].title }}</h5>
    <p>{{ posts[$route.params.id].content }}</p>
    <p>{{ posts[$route.params.id].date }}</p>
    <p>{{ posts[$route.params.id].number }}</p>
  </div>
</template>

<script>
export default {
  name: "Detail",
  props: {
    posts: Array
  },
}
</script>

<style>

</style>
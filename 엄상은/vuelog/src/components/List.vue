<template>
  <div>
    <h5>{{ post.title }}</h5>
    <p>{{ post.date }}</p>
  </div>
</template>

<script>
export default {
  name: 'List',
  props: {
    post: Object
  }
}
</script>

<style>

</style>
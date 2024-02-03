<template>
  <div>
    <Post v-for="(x, i) in posts" :key="i" :post="x"/>
  </div>
</template>

<script>
import Post from './Post.vue';

export default {
  components: {
    Post: Post
  },
  props: {
    posts: Array
  }
}
</script>

<style>

</style>
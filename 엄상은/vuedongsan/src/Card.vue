<template>
  <div>
    <img class="room-img" :src="room.image" />
    <h4 @click="$emit('openModal', room.id)">{{ room.title }}</h4>
    <p>{{ room.price }}</p>
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
    room: Object
  }
}
</script>

<style>

</style>
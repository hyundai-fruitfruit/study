
# VUE STUDY 정리

### 전체 구조 및 데이터 바인딩

```
// HTML
<template>
    <div>
			<p>{{ price1 }} 만원</p> // 데이터 바인딩
    </div>
</template>

<script>


// JS
export default {
  name: 'App',
  data() { // 데이터 담는 곳
    return {
      price1 : 100
    } 
  },
  components: {
  }
}
</script>

// CSS
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
### 

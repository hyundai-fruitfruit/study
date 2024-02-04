<template>
  <div class="header">
    <ul v-if="step==1||step==2" @click="step--" class="header-button-left">
      <li>Cancel</li>
    </ul>
    <ul class="header-button-right">
      <li v-if="step==1" @click="step++">Next</li>
      <li v-if="step==2" @click="publish">Post</li>
    </ul>
    <img src="./assets/logo.png" class="logo" />
  </div>

  <Container :posts="posts" :step="step" :url="url" @updateContent="myContent=$event"/>
  <button @click="more()">더보기</button>

  <div class="footer">
    <ul class="footer-button-plus">
      <input @change="upload" type="file" id="file" class="inputfile" />
      <label for="file" class="input-plus">+</label>
    </ul>
  </div>
</template>

<script>
import posts from './data/posts.js'
import Container from './components/Container.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    Container: Container
  },
  data() {
    return {
      posts: posts,
      moreCount: 0,
      step: 0,
      url: "",
      myContent: "",
    }
  },
  methods: {
    more() {
      if (this.moreCount == 0) {
        axios.get("https://codingapple1.github.io/vue/more0.json")
        .then((result) => {
          console.log(result)
          this.posts.push(result.data);
        })
      }
      else {
        axios.get("https://codingapple1.github.io/vue/more1.json")
        .then((result) => {
          console.log(result)
          this.posts.push(result.data);
        })
      }
      this.moreCount++;
    },
    upload(e) {
      let file = e.target.files;
      this.url = URL.createObjectURL(file[0]);
      this.step++;
    },
    publish() {
      var myPost = {
        name: "tori",
        userImage: this.url,
        postImage: this.url,
        likes: 0,
        date: "Feb 3",
        liked: false,
        content: this.myContent,
        filter: "perpetua"
      };
      this.posts.unshift(myPost);
      this.step = 0;
    }
  }
}
</script>

<style>
body {
  margin: 0;
}
ul {
  padding: 5px;
  list-style-type: none;
}
.logo {
  width: 22px;
  margin: auto;
  display: block;
  position: absolute;
  left: 0;
  right: 0;
  top: 13px;
}
.header {
  width: 100%;
  height: 40px;
  background-color: white;
  padding-bottom: 8px;
  position: sticky;
  top: 0;
}
.header-button-left {
  color: skyblue;
  float: left;
  width: 50px;
  padding-left: 20px;
  cursor: pointer;
  margin-top: 10px;
}
.header-button-right {
  color: skyblue;
  float: right;
  width: 50px;
  cursor: pointer;
  margin-top: 10px;
}
.footer {
  width: 100%;
  position: sticky;
  bottom: 0;
  padding-bottom: 10px;
  background-color: white;
}
.footer-button-plus {
  width: 80px;
  margin: auto;
  text-align: center;
  cursor: pointer;
  font-size: 24px;
  padding-top: 12px;
}
.sample-box {
  width: 100%;
  height: 600px;
  background-color: bisque;
}
.inputfile {
  display: none;
}
.input-plus {
  cursor: pointer;
}
</style>

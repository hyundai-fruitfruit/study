# Part 3: 인스타그램 만들기

## 21. vuestagram layout

### 컴포넌트화의 기준

- 다른 곳에서 쓸 부분
- 라우터로 나눌 페이지 부분
- HTML 너무 길어서 복잡한 부분

## 22. homework

### 인라인스타일에 변수 넣기

- 변수와 문자를 같이 넣어줘야 하기 때문에 복잡함
    - `'문자' + 변수 + '문자’` 이런 식
- 스타일 태그 안에 Object 자료형도 넣을 수 있음
    - { 스타일 속성명: 값 }
    - 하지만 javascript에서 대쉬(-)를 오브젝트 이름으로 쓸 수 없기에 CamelCase로 변환
    - { backgroundImage: ‘url(https://picsum.photos/100?random=0)’ }
        - 그 안에 변수를 쓰고싶다면 ES6 문법으로 다음과 같이 변경
        - `:style="{ backgroundImage: `url(${post.postImage})`}"`

## 23. ajax with axios

### ajax 요청

- GET, POST 요청하는 방법
    - 주소창에 넣거나 form으로 보내기 → 브라우저가 새로고침됨
    - ajax 요청 → 브라우저가 새로고침되지 않음
- ajax 요청을 하려면
    - ***방법 1) axios 라이브러리 쓰기***
    - 방법 2) 기본 fetch 함수 쓰기

### axios 라이브러리 설치하고 사용하기

- `npm install axios`

```jsx
import axios from 'axios';

axios.get()
axios.post()
```

### GET 요청 받아오는 함수 만들기

```jsx
more() {
  axios.get("https://codingapple1.github.io/vue/more0.json")
  .then(function(result) {
    console.log(result)
  })
}
```

- `function(){}` 대신에 `()=>{}`를 쓰는 것이 좋음
    - Vue에서 데이터를 가져다 쓰기 위해 this 예약어를 사용하는데, 일반함수는 this를 재정의함
    - arrow function을 쓰면 this를 그대로 쓸 수 있음
        - 또한, 소괄호 안에 변수 하나라면 소괄호 생략 가능

```jsx
more() {
  axios.get("https://codingapple1.github.io/vue/more0.json")
  .then((result) => {
    console.log(result)
    this.posts.push(result.data);
  })
}
```

- 실시간 렌더링을 지원하기 때문에 posts 안에만 넣어주면 동작함

### POST 요청 날리기

- axios.post(’url’, {name: ‘kim’}).then().catch()
- 성공 시 실행할 부분은 .then()으로 넘어옴
- 실패 시 실행할 부분은 .catch()으로 넘어옴
    - 콜백함수를 하나 추가해주면 에러 메세지가 함께 날아옴

## 24. tabs

### tab을 이용해 컨텐츠를 바꾸어 보여주기

- 동적인 UI 구성
    - 상태를 저장할 변수 data에 저장
    - 상태에 따라 보여지는 값 지정
    - 상태를 변경할 액션 지정
- 다른 페이지가 필요하면 vue-router 써도 되지만 간단한 UI는 탭으로도 가능
    - vue-router의 장점: 뒤로가기 등의 액션 가능

## 25. file upload

### 이미지 업로드한 걸 HTML에 보여주려면?

- 브라우저에서 이미지를 다루는 함수를 써서 서버를 보내기 전에 보여주거나 조작할 수 있음
    - 방법 1) FileReader()
        - 이미지를 글자로 변환 (저장하고 넣을 수 있음)
    - 방법 2) URL.createObjectURL()
        - 이미지 URL을 잠깐 만들어줌 (새로고침 시 사라짐)

### blob 파일

- 이미지 또한 0과 1로 이루어진 binary 데이터
- 이미지를 BLOB(Big Large Object)이라는 object에 담아서 브라우저에서 담음
- 이미지를 쪼개거나 확장자를 변경하는 등의 조작이 가능함

### input 속성

- 입력을 여러 개 받고자 한다면 `<input multiple />` 로 받아야 함
- 이미지만 보이게 만들고 싶다면 `<input accept=”image/*”>` 설정
    - 이미지만 업로드받음을 보장하는 건 아님
    - 파일.type으로 받아와서 추가적으로 제한 필요

## 26. add post

### 글 발행버튼 만들기

- 글 발행 버튼의 위치: `App.vue`
- 글 내용 인풋의 위치: `Container.vue`
- 글 발행 버튼이 눌리면 글 내용을 받아와서 `posts` 라는 state에 넣어줘야 함
    - 자식 → 부모 데이터를 보내려면 `$emit` 이용
        - `$emit` 이용법
            - 자식: `$emit(’작명’, 보낼 것)`
            - 부모: `@작명=”일어날 일”` , `$event`에 ‘보낼 것’ 담김

### Container.vue

```html
<!-- 글작성페이지 -->
<div v-if="step==2">
  <div class="upload-image" :style="{ backgroundImage: `url(${url})`}"></div>
  <div class="write">
    <textarea v-model="content" @change="$emit('updateContent', content)" class="write-box">write!</textarea>
  </div>
</div>
```

- v-model로 content에 넣고, 그것을 `@change` 발동시켜 담았지만, 다음과 같은 코드가 더 간편하게 처리 가능함
    
    ```html
    <textarea @input="$emit('write', $event.target.value)" class="write-box">write!</textarea> 
    ```
    

### App.vue

```jsx
<template>
  <Container :posts="posts" :step="step" :url="url" @updateContent="myContent=$event"/>
</template>

<script>
import posts from './data/posts.js'
import Container from './components/Container.vue';

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
</script>

<style>
...
</style>
```
# Part. 1

Why Vue?

- **쉬워서**
    - 그대신 이상한거 아님 ?
        - ㄴㄴ 문법만 다름
- 정해져있음
    - `<HTML>`을 여러개 쓰고싶을때
        - React는 방법이 여러개
        - Vue는 v-for 하나밖에 없음
        - Vue 문법 몇개 외워주면 초보도 쉽개 output냄
- HTML 렌더링이 리액트보다 더 빠름
- 업데이트 잘됨

---

npm install -g @vue/cli@4.5.11

- vue cli 설치
    - vue 개발환경 세팅에 도움주는
- Vue 프로젝트 생성
    - vue create vuedongsan

```sql
<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

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
```

- `<template>` 안에는 HTML
- `<script>` 안에는 JS
- `<style>` 안에는 CSS

미리 보기는

- npm run serve

### 파일 구조

node_modules : 프로젝트에 쓰는 라이브러리들

src : 소스코드 다 담는 곳

public: html 파일, 기타파일 보관

package.json : 라이브러리 버전, 프로젝트 설정 기록

---

### HTML에 데이터 꽂아넣는 Vue 데이터바인딩 문법

### 데이터 바인딩

- JS 데이터를 HTML에 꽂아넣는 문법

```jsx
data(){
    return {
      object1 : 500,
    }
  },
```

- 데이터 보관함

HTML에 데이터를 바인딩 하고 싶다면

```jsx
<p> {{ object1 }} </p>
```

### 데이터 바인딩 쓰는 이유

1. 실시간
2. HTML 변경이 어려움

HTML 속성도 데이터바인딩 가능

- **:속성=”데이터이름”**

---

### Vue 반복문

array/object 집어넣기 가능

- 그럼 자료안의 데이터 갯수만큼 반복

Ex )

```jsx
<a v-for="작명 in 메뉴들" :key="작명">{{작명}}</a>

1. 자료안의 데이터 갯수만큼 반복됨
2. 작명한 변수는 데이터안의 자료가 됨
```

- :key=””의 용도
    - 반복문쓸 때 꼭 써야함
    - 반복문 돌린 요소를 컴퓨터가 구분하기 위해 씀

```jsx
<a v-for="(a,idx) in 메뉴들" :key=idx>{{a}}{{idx}}</a>
```

---

### **Vue 이벤트 핸들러로 click 감지하기 (허위매물 신고버튼 만들기)**

```jsx
<button v-on:click="abc"></button>

OR

<button @click>"abc"="abc"></button>
```

말고도 여러가지 이벤트 사용가능

- @mouseover
    - 마우스를 위에 올렸을때

---

### v-if와 모달창 만들기(vue에서 동적인 UI 만드는 법)

### 동적인 UI 만드는법 :

1. UI의 현재 상태를 데이터로 저장해둠
2. 데이터에 따라 UI가 어떻게보일지 작성

```jsx
v-if="1==1"

조건식이 참일때만 HTML 보여줌
```

---

### **모달창 내에 상세페이지 만들기**

== 동적인 UI만드는 법

```jsx
<div v-if="1 == 2">
  안녕하세요
</div>
<div v-else>
  안녕하세요2
  </div>
```

- 참이 아니면 안녕하세요2 들장

---

### Component

src내에 vue파일 만들고

그 다음에 축약할 HTML 넣기

축약해둔 컴포넌트 쓰는법

1. vue 파일 Import
2. 등록(import)
3. 사용
    1. `<Discount/>`
    2. `<Discount></Discount>`

### 반복적인 UI들을 축약할때 장점

### 데이터 관리가 힘든점이 단점

---

### 부모가 가진 데이터를 자식이 사용하고 싶으면 props

사용법

1. 데이터를 보냄
2. 등록
3. 사용
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
`Ex ) <Modal :원룸들="원룸들" />`

데이터는 한 곳에 보관하고

→ 필요하면 가져다 씀(props)

사이드바 열기/닫기

- cmd + B

**props는 read-only임 받아온거 수정 XX**

데이터를 쓰는 곳이 여러 파일이라면 가장 부모 컴포넌트에 만들어주면됨

- Why ?
    - 자식에서 부모 컴포넌트로 데이터를 전송하기는 까다로운 문법이 동반됨 But, 부모에서 자식 컴포넌트로 데이터를 보낼때는 (props !)

---

![스크린샷 2024-02-01 오후 9.07.39.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/2609b706-5673-4fec-b2bc-2b7fdfe2c8bf/b140c308-2db8-4e87-9d18-7ab808605896/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-02-01_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_9.07.39.png)

---

### Custom Event

- 자식 요소에서 부모 요소에 데이터를 변경할때

**props로 보낸 데이터는 수정금지 !!!**

부모에게 메세지 보낼땐

1. 자식은 $emit(’작명’,데이터)
2. 부모는 메세지받으려면 @작명한거=”

자식이 보낸 데이터는 $event 변수에 담겨있음

---

### 사용자의 input을 받는 법 (v-model)

Ex ) 

```jsx
<input @input="month = $event.target.value">

<p> {{month}}개월 선택함 : {{원룸들[누른거].price * month}}원</p>
```

```jsx
data(){
    return{
      month : 1,
    }
  },
```

유저가 <input>에 입력한 값을 데이터로 저장하는 법2

**v-model**

```jsx
<input v-model="month">
```

- 위에 코드와 동일

초기값이 중요 ! 

- 문자로 받을거냐
- 자연수로 받을거냐
- …

---

### watcher로 데이터 감시하는 법

input에 문자 입력하면 경고문을 띄우고 싶다.

- watcher (data 감시하는 함수)

```jsx
data(){
    return{
      month : 1,
    }
  },
  watch : {
    month(){
      
    }
  }
```

- month 데이터가 변할 때마다 watcher도 실행됨

데이터 감시하려면

watch : { 감시할데이터(){} }

---

### Vue에서 UI 애니메이션 주는 법

1. 애니메이션 주고 싶은 요소를 <transition>
    1. <transition name=”작명”>으로 감싸기
2. class명 3개 작성

```jsx
.fade-enter-from{시작스타일}
.fade-enter-active{transition}
.fade-enter-to{끝 스타일}
```

---

### 상품정렬기능과 데이터 원본 보존

- sort() : 원본 변형
- map() or filter() : 원본 변형 X

---

### Vue의 Lifecycle

컴포넌트의 lifecycle

- 배우는 이유 : Lifecycle Hook을 쓰려고 배움

<컴포넌트>는 웹페이지에 표시되기까지 일련의 step을 거침

- 그 step을 라이프사이크이라고함

**크게 4단계**

1. create단계
    1. 데이터만 존재하는 단계
2. mount단계
    1. <template> 사이에 있던걸 실제 HTML로 바꿔줌
3. 컴포넌트 생성
    1. index.html에 장착
4. update 단계
    1. data가 변하면 HTML이 재렌더링 된다고 했었음
    2. data가 변하면 실은 <컴포넌트>가 재렌더링됩니다.

![스크린샷 2024-02-03 오후 9.42.29.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/2609b706-5673-4fec-b2bc-2b7fdfe2c8bf/803ea396-a7ef-4807-bb22-bf2461815882/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-02-03_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_9.42.29.png)

![스크린샷 2024-02-03 오후 9.24.32.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/2609b706-5673-4fec-b2bc-2b7fdfe2c8bf/d80519e4-c3a1-4386-9174-b81ec0f049b4/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-02-03_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_9.24.32.png)

- 서버에서 데이터 가져올때도 lifecycle hook 안에 코드 짬
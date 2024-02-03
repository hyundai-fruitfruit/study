# Part 2: blog 레이아웃과 라우터

## 16. bootstrap

### 새 프로젝트 만들기

- `vue create vuelog`

### 부트스트랩 설치하기

- 방법 1) css, js 파일 복붙으로 설치
    - https://getbootstrap.com/docs/5.3/getting-started/download/#compiled-css-and-js
    - 버전 체크 후 `index.html`에 css, js 복붙
    - 단점
        - 로딩이 오래 걸릴 수도 있음 → 다운로드 후 넣어도 됨
- 방법 2) npm 으로 설치
    - `npm install bootstrap@5`
        - 정확한 명령어는 사이트에서 확인
    - `npm run serve` 종료 후 해야 함
    - `main.js` 에 import문 추가
        
        ```jsx
        import 'bootstrap'
        import 'bootstrap/dist/css/bootstrap.min.css'
        ```
        

## 17. blog data binding

### List.vue로 컴포넌트 분리하고 데이터 가져오기

`List.vue`

```jsx
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
...
</style>
```

`App.vue`

```jsx
<template>
  <List v-for="(x, i) in posts" :key="i" :post="posts[i]"/>
</template>

<script>

import posts from './data/posts'
import List from './components/List.vue'

export default {
  name: 'App',
  data() {
    return {
      posts: posts
    }
  },
  components: {
    List: List
  },
}
</script>

<style>
...
</style>
```

### 복습

- props 이용하기
    - props로 보낼 땐 `:작명=”데이터”`
    - 자식 컴포넌트에서 props 등록
        - `props: { 작명: 타입 }`
- js 파일로 저장된 데이터 가져오기
    - `export default …`
    - `import 작명 from 위치`

## 18. vue-router

### vue-router 설치

- `npm install vue-router@4`
- 다시 시작 후 라이터 설정
    - `main.js` 에서 사용할 `router.js` 만들기
    
    ```jsx
    import { createWebHistory, createRouter } from "vue-router";
    
    const routes = [
      {
        path: "/경로",
        component: import해온 컴포넌트,
      }
    ];
    
    const router = createRouter({
      history: createWebHistory(),
      routes,
    });
    
    export default router;
    ```
    
    - `main.js` 에서 이용하기
    
    ```jsx
    import router from './router'
    
    createApp(App).use(router).mount('#app')
    ```
    

### 라우팅하기

- 만든 라우팅이 뜰 수 있도록 해야함
- `App.vue`에 router-view 태그로 구성
    
    ```jsx
    <router-view :key="i" :posts="posts"></router-view>
    ```
    
    - 똑같이 props 넘길 수 있음
- 편의를 위한 링크 생성하기
    - `<router-link to="/">홈페이지</router-link>`

## 19. route params

### URL의 parameter 이용하기

- `route.js`
    
    ```jsx
    import Detail from './components/Detail.vue'
    
    const routes = [
      ... ,
      {
        path: "/detail/:id",
        component: Detail,
      },
    ];
    ```
    
- `$route.params` 로 파라미터를 꺼내쓸 수 있음
    - `<h5>{{ posts[$route.params.id].title }}</h5>`

### 파라미터 문법

- 정규식 입력 가능
    - `path: "/detail/:id(\\d+)”`
        - 정수만 받고 싶을 경우
    - `path: "/detail/:id*”`
        - 반복되는 경우
    - vue-router 4 문서 참고
        - https://next.router.vuejs.org/
    - 응용 시 404 페이지 만들기 가능
        
        ```jsx
        {
          path: "/:anything(.*)",
          component: Home,
        }
        ```
        
- 라우터의 경우 위에서 먼저 선언된 부분이 우선권을 가짐

## 20. nested routes / push

### 필요한 상황

- 디테일 페이지 안에서 세부적인 UI를 만들고 싶을 때 nested routes로 할 수 있음
    - detail/0/author, detail/0/comment 등

### 방법

- routes 안에 children 만들기
    - path 안에는 상대경로로 적어줘야 함 (예: path: “author”)
    
    ```jsx
    {
      path: "/detail/:id(\\d+)",
      component: Detail,
      children: [
        {
          path: "author",
          component: Author
        },
        {
          path: "comment",
          component: Comment
        }
      ]
    },
    ```
    
- 각 vue를 어디서 보여줄 지도 정해야 함
    - Detail에서 `<route-view />`로 보여주기

### 페이지 연결하기

- 방법 1) `<router-link>` 이용
- 방법 2) `@click=”$router.push(/detail/0)”` 이용

### $route

- 현재 URL에 관련 기능
- $route.fullPath

### $router

- 페이지 이동 관련 기능
- $router.go(1)
    - 앞으로 가기
- $router.go(-1)
    - 뒤로 가기

### 라우팅 시 여러 개의 컴포넌트를 보여주고 싶을 때

```jsx
{
  path: "/list",
  component: {
    List: List,
    Comment: Comment,
  },
},
```

## *. hash mode, guards

### hash mode vs HTML5 mode

- HTML5 mode (이전 설정)
    
    ```jsx
    import { createRouter, createWebHistory } from 'vue-router'
    
    const router = [];
    const router = createRouter({
      history: createWebHistory(),
      routes,
    })
    ```
    
    - URL에 입력된 값은 Vue router로 보여지는 것이 아니라 서버에서 요청받는 것
    - 이 때문에 라우팅 전에 서버가 해당 페이지를 보여주려고 할 수 있음
    - 하지만 기능 개발을 안 해놨으니 404 페이지가 뜰 수도 있음
    - 이를 방지하려면 createWebHistory 대신 createWebHashHistory 사용 가능 (hash mode)
- hash mode
    - URL에 전부 #이 붙은 채로 시작
    - \# 뒤의 내용은 절대 서버로 전달되지 않음
    - vue router에게 온전히 라우팅을 맡기는 것

### Navigation guards

- hook 같은 기능
    - 라우팅 전에 확인
- /hello 경로로 들어가기 전에 검사를 해주고 싶다면 beforeEnter 항목 이용
    
    ```jsx
    const routes = [
      {
        path: "/hello",
        component: HelloWorld,
        beforeEnter: ()=>{
          if (로그인했냐 == false) {
            return '/login'
          }
        }
      }
    ];
    ```
    
    - 서버에서도 검증 필요
    - 파라미터로 두세개 넣을 수 있음 (to, from)과 같은 형태
        - 이들은 $route 타입
            - to.fullPath나 to.params.id 등을 이용 가능
    - 리턴값
        - 없으면 원래 페이지
        - false이면 라우팅 중단

### 여러 개의 route에 같은 navigation guard를 추가하고 싶을 때

- router라는 변수에 .beforeEach() 같은 함수를 이용
- 라우팅 전에 실행할 일
    - beforeEach()
    - beforeResolve()
- 라우팅 이후 실행할 일
    - afterEach()

### 컴포넌트 안에서도 navigation guard 이용 가능

- beforeRouteEnter(){}나 beforeRouteUpdate(){}를 lifecycle hook 위치에 적용
    - 파라미터 두 개 입력 가능 (to, from)
- 특정 페이지로 접속 시 ajax 요청할 일이 있다면 저기에 쓰자

## *. build

### 빌드하기

- `npm run build` 혹은 `yarn build`
- dist 안에 index.html, css 파일과 js 파일이 생성됨
- 이들을 서버에 올리기

### GitHub pages에 올리기

- `아이디.github.io` 로 레파지토리 만들기
- dist의 내용물을 올리고 사이트 확인 (https://아이디.github.io)
- 서브경로에 발행하고 싶을 경우에는 추가 설정 필요 
# Part 1: 부동산 쇼핑몰

## 1. setting up

### 개발환경 셋팅과 Vue 3 설치

- node.js 설치
- Visual Studio Code 설치
- Vue 개발환경 세팅을 도와주는 Vue Cli 설치
    - `npm install -g @vue/cli`
- VS Code Extension 설치
    - Vetur
    - HTML CSS Support
    - Vue 3 Snippets

### 뷰 프로젝트 생성

- `vue create vuedongsan`
- 프로젝트 서버 실행
    - `npm run serve`
- main.js가 App.vue → index.html 하는 과정을 담당
- package.json: 라이브러리 버전, 프로젝트 설정 기록 보관

## 2. Data binding

### 데이터바인딩

- JS 데이터를 HTML에 꽂아넣는 문법
- Vanilla JS 스타일 데이터 바인딩
    - `documnet.getElementById(??).innerHTML = ??`
- 데이터 보관함 (중요한 변수들 보관)
    - 데이터는 Object 자료형으로 저장
        
        ```jsx
        data() {
          return {
        		price1: 60,
        	}
        },
        ```
        
    - 데이터 이용 시 데이터 이름을 사용
        - `{{ price1 }}`

### 데이터바인딩을 하는 이유

- HTML 변경을 용이하게 하도록 하기 위해
- ***Vue의 실시간 자동 렌더링*** 쓰기 위해
    - data를 변경 시에 data와 관련된 HTML도 실시간으로 반영됨
    - 웹앱 같은 사이트를 만들기 용이함
    - 실시간으로 바뀔 일이 없는 값은 하드코딩
    - HTML 속성도 데이터 바인딩 가능
        - `:속성=”데이터이름”`
        - `<h4 class="red" :style="스타일">{{ products[0] }}</h4>`

## 3. v-for

### HTML 반복문으로 상단 메뉴 만들기

- `<태그 v-for="작명 in 횟수" :key="작명">`
- `<태그 v-for="작명 in 자료형" :key="작명">`

```jsx
<template>
  <div class="menu">
    <a v-for="x in 메뉴들" :key="x"> {{ x }} </a>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      메뉴들: ['Home', 'Shop', 'About'],
    }
  },
  components: {
  }
}
</script>
```

### v-for 안에 변수를 2개까지 작명하기

- `:key=””` 의 용도
    - 반복문 쓸 때 꼭 써야 함
    - 반복문 돌린 요소를 컴퓨터가 구분하기 위해 씀
- `<a v-for="(x, i) in 메뉴들" :key="i"> {{ x }} </a>`
    - 왼쪽 변수는 array 내의 데이터
    - 오른쪽 변수는 1씩 증가하는 함수

## 4. event handler

### 버튼 온클릭 리스너

- `v-on:click=””`
- `@click=””`

### 허위매물 신고 시 숫자 1 증가하도록 설정

```jsx
<button v-on:click="count++">허위매물신고</button> <span>신고수: {{count}}</span>
```

### 다른 이벤트 핸들러

- @mouseover
    - 마우스만 댔을 때
- @input
    - 인풋에 값을 입력했을 때
- @drag
- …

### 함수

- methods: {} 항목에 넣기
- this.변수명으로 사용
    - 데이터와 함수를 담은 큰 오브젝트를 this

## 5. v-if / modal

### 이미지를 넣는 법

- `<img class="room-img" src="./assets/room0.jpg" />`
- assets에 저장

### Vue로 동적인 UI를 만드는 방법

- (0) UI로 만듦
- (1) 현재 HTML UI의 상태를 데이터로 저장해둠
    - (모달창이) 지금 보이는지 안 보이는지
- (2) 그 상태에 따라 HTML UI를 보여주지 말지를 Vue 문법으로 작성

### state

- data 저장 공간

## 6. import export

### import / export 하기

- 방법1
    - export default 변수명
    - import 변수명 from 그파일경로
- 방법2
    - export {변수1, 변수2}
    - import {변수1} from 그파일경로

## 7. product detail

### 모달의 상세페이지 구성

- 누른 상품에 해당하는 상세페이지 내용으로 구성함

```jsx
<template>
  <div class="black-bg" v-if="is_modal_open == true">
    <div class="white-bg">
      <h4>{{ oneroom[id].title }}</h4>
      <p>{{ oneroom[id].content }}</p>
      <button v-on:click="is_modal_open = false">닫기</button>
    </div>
  </div>

  <div class="menu">
    <a v-for="a in menu" :key="a"> {{ a }} </a>
  </div>

  <div v-for="(x, i) in oneroom" :key="i">
    <img class="room-img" :src="oneroom[i].image" />
    <h4 v-on:click="is_modal_open = true; id = i">{{ oneroom[i].title }}</h4>
    <p>{{ oneroom[i].price }}</p>
    <button v-on:click="increase(i)">허위매물신고</button> <span>신고수: {{ counts[i] }}</span>
  </div>
</template>

<script>

import data from './data/oneroom'

export default {
  name: 'App',
  data() {
    return {
      is_modal_open: false,
      menu: ['Home', 'Shop', 'About'],
      counts: [0, 0, 0, 0, 0, 0],
      oneroom: data,
      id: null
    }
  },
  components: {
  },
  methods: {
    increase(x) {
      this.counts[x]++
    }
  }
}
</script>

<style>
...
</style>
```

### v-if / v-else

- <div v-if=”조건”></div>
- <div v-else-if=”조건”></div>
- <div v-else></div> 도 가능

## 8. component

### 컴포넌트

- 원하는 HTML 덩어리를 한 글자로 축약할 수 있게 도와주는 문법
- 컴포넌트 만들기
    - 파일을 새로 생성 (Discount.vue)
    - 파일 형식이 정해져있음
        - Extension으로 < + enter로 포맷 사용 가능
        - template 안에 원하는 html 넣기
        - name 속성 안에 이름 적기
- 컴포넌트 가져다 쓰기
    - (1) vue 파일 import 하기
        - import Discount from 경로;
    - (2) components 오브젝트 안에 등록하기
        - Discount: Discount,
        - 둘의 이름이 같다면 축약이 가능함
            - Discount,
    - (3) 쓰기
        - <Discount />

### 컴포넌트.vue 이름의 규칙

- 두 단어로 작명 필요
- 이 옵션을 무시하고 싶다면 package.json에서 항목 추가
    
    ```json
    "rules": {
       "vue/multi-word-component-names": "off"
    }
    ```
    
- 추가하고 다시 시작

### 컴포넌트를 사용하는 이유

- 심미적 이유
- 재사용이 쉬움
- 나중에 라우터로 페이지를 구분하고 싶으면 하나의 페이지는 하나의 컴포넌트로 구성하는 것이 좋음

### 컴포넌트의 단점

- 데이터바인딩 시 귀찮은 문제가 생길 수 있음
    - 아무때나 컴포넌트화를 하면 안 됨

## 9. props

### 컴포넌트화할 경우의 데이터

- 데이터바인딩은 밑에 데이터가 있어야 가능함
- 데이터를 복사 붙여넣어서 쓸 수는 없음
- props를 이용해 넘겨줌
    - 자식이 부모가 가진 데이터를 쓸 경우
    - App.vue (부모 컴포넌트), Modal.vue (자식 컴포넌트)

### props를 사용하는 과정

- (1) 보내기
    - `<자식 :데이터=”데이터”>`
    - `<자식 v-bind:데이터=”데이터”>`
- (2) 등록하기
    - props에 정의
        
        ```jsx
        export default {
          name: 'Modal',
          props: {
            oneroom: Array,
            id: Number,
            is_modal_open: Boolean,
          },
        }
        ```
        
    - 하지만 props는 read-only. 재할당 불가능
- (3) 사용하기

### 자식 컴포넌트에서의 데이터

- 데이터를 만들어도 됨
- 하지만 부모도 쓰는 데이터라면 부모 컴포넌트에 만들기
    - 위로 전송하는 방법이 어려움

## 10. homework & props 2

### 오브젝트를 props로 보내기

- `<Discount v-bind=”오브젝트” />`

### Card의 컴포넌트화

- `App.vue`
    
    ```jsx
    <template>
      <Card v-for="(x, i) in oneroom" :key="i" :room="oneroom[i]"/>
    </template>
    
    <script>
    
    import data from './data/oneroom'
    import Card from './Card.vue'
    
    export default {
      name: 'App',
      data() {
        return {
          oneroom: data,
        }
      },
      components: {
        Card: Card,
      },
    }
    </script>
    
    <style>
    
    ...
    
    </style>
    ```
    

- `Card.vue`
    
    ```jsx
    <template>
      <div>
        <img class="room-img" :src="room.image" />
        <h4>{{ room.title }}</h4>
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
    ```
    

## 11. custom event

### 자식이 부모데이터를 바꾸고 싶을 때

- props로 전달받은 것은 수정이 불가능 (read-only)
- custom event로 메세지를 전해줌
- 우리가 해결하고자 하는 모달창 이슈는 Card 컴포넌트에 onclick을 먹여도 해결되긴 함
    - 이벤트 버블링 현상 때문
    - 하지만 다른 방법을 사용하기로 함

### custom event

- 자식 → 부모로 메세지를 보내서 값을 변경할 수 있도록 함
- $emit(’작명’, 데이터)
    - $: Vue만의 특별한 변수
    - 부모까지 메세지를 발생시킬 수 있음
    

### 동작 방식

- 부모에게 메세지 보낼 때
    - $emit(’작명’, 데이터)
- 부모가 메세지 수신할 때
    - @작명한거=””
    - $event
        - 자식이 보낸 데이터도 함께 확인

### 함수로 분리하고 싶다면

- this.$emit()으로 사용해야 함
- 안에 사용되는 매개변수도 this.변수 형태로 사용

## 12. v-model

### 사용자의 input 받는 법

- `@input`
    - 사용자 입력 시 이벤트 리스너
- `$event`
    - event object
    - 자바스크립트 이벤트리스너에서 addEventListener('click', function(e){})의 e와 같은 의미
- `$event.target`
    - 현재 이벤트가 일어나고 있는 요소
- `$event.target.value`
    - 인풋에 입력한 값

### v-model

- 입력된 값을 데이터로 바로 저장할 수 있도록 함
- `<input v-model="month">`
    - `<input @input="month = $event.target.value">`와 같은 의미
- textarea, select 등에도 모두 적용 가능
    - month와 같이 데이터로 저장할 부분의 초기값을 잘 선택해줘야 함
        - 숫자 초기값을 잡을 경우 텍스트가 들어올 때 못 잡을 수 있음
        - 하지만 숫자 인풋이 들어와도 문자자료형
        - 곱셈의 경우에는 잘 인식하지만 덧셈은 잘 못 해줌
            - `v-model.number=”month”` 이용하여 문자로 인식할 수 있도록 해줌

## 13. watch

### watcher를 이용해 데이터를 감시

- input에 문자를 입력하면 경고문을 띄워보자
- watch 오브젝트 생성
    - month() {}
        - month 데이터가 변할 때마다 watcher도 실행됨

```jsx
watch: {
    month(a) {       
        if (a >= 13) {
            alert("13 미만의 숫자를 입력해주세요");
            a = 1;
        }
    },
},
```

- a는 month가 변경될 값
- month(a, b)에서 b는 변경 전 값

## 14. transition

### CSS로 애니메이션 주기

- 시작 전 class 명
- 애니메이션 끝난 후 class명
- 그리고 원할 때 2번 class명 부착

### 과정

- 시작 전과 후의 class를 디자인

```jsx
.start {
  opacity: 0;
  transition: all 1s;
}

.end {
  opacity: 1;
}
```

- 조건부로 class를 붙여줄 수 있도록 함
    
    ```jsx
    <div class="start" :class="{ end: true }">
    ```
    
    - end라는 클래스명이 true일 때만 붙음

### Transition 태그로 애니메이션 주기

- (1) 애니메이션 주고 싶은 요소를 <Transition name=”작명”>으로 감싸기
- (2) class명 3개 작성
    
    ```jsx
    <style>
    .fade-enter-from {
      opacity: 0;
    }
    .fade-enter-active {
      transition: all 1s;
    }
    .fade-enter-to {
      opacity: 1;
    }
    ```
    
    - 작명-enter-from { 시작스타일 }
    작명-enter-active { 애니메이션 동작 상태 }
    작명-enter-to { 끝스타일 }
    - 퇴장 애니메이션은 ‘leave’

## 15. sort

- 기존 vanilla JS의 경우 정렬을 한다면 정렬 후 HTML에 업데이트하는 과정이 필요하지만 Vue.js를 이용하면 그 과정이 필요 없음
    - 자동으로 데이터 바인딩이 되어있기 때문

### 숫자 순 정렬

```jsx
var array = [2,5,1];
array.sort(function(a,b){
  return a - b
});
```

- 음수면 a를 왼쪽으로 보내달라는 식으로 동작

### 가격 순 정렬

```jsx
priceSort() {
  this.oneroom.sort(function(a, b) {
    return a.price - b.price
  })
}
```

### 되돌리기 구현

- sort()는 원본이 변할 수 밖에 없음
- oneroom_orig을 두도록 함
    - 그냥 같은 값을 가져가면 안되고 deepcopy 진행 필요

## 16. lifecycle hooks

### 컴포넌트의 lifecycle

- 생명주기를 알고 특정 생명주기 전과 후에 hook을 걸 수 있음

![image](https://github.com/hyundai-fruitfruit/study/assets/63828057/5aef0325-64c3-41bb-955c-701ae9695cf5)

- create 단계
    - 데이터만 존재하는 단계
- mount 단계
    - `<template>` 사이에 있던 것을 실제 HTML로 바꿔줌
- 컴포넌트 생성
    - 그다음에 index.html에 장착함
- update 단계
    - data가 변하면 HTML이 재렌더링
    - 실은 컴포넌트가 재렌더링 되는 과정
- unmount 단계
    - 컴포넌트가 사라질 때

### 할인 창이 2초 후에 사라지게 하려면

- 동적인 UI 만드는 법 이용
    - 새로운 state를 정의하고 해당 창이 state 값에 따라 나타나게 함 (v-if)
- 타이머 이용
    
    ```
    setTimeout(function() {
    	실행할 내용
    }, 2000);
    ```
    
- this를 붙일 때 그냥 함수 대신 () =>{} 함수로 사용
    - 바깥의 this를 제대로 가져다 쓸 수 있음
- mounted() 정의
    - components에 같은 레벨로 정의
    
    ```jsx
    mounted() {
      setTimeout(() => {
        this.showDiscount = false;
      }, 2000);
    },
    ```
    

### 모든 컴포넌트에 다 붙일 수 있음

- App.vue에 mount() 사용하면 App.vue가 mount되자마자 코드 실행
- Modal.vue에 mount() 사용하면 Modal.vue가 mount되자마자 코드 실행

### 서버에서 데이터를 가져올 때

- 이 때에도 created(), mounted() 중 하나를 요청해 이 안에서 서버에서 데이터 가져오는 코드를 작성함
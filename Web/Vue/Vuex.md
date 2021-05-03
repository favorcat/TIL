# App.vue에서 상태 관리 패턴 사용하기
App.vue에서 다른 vue 컴포넌트 파일을 참조하는 경우 한 변수를 여러 곳에서 사용하고 싶을 때 상태 관리 패턴을 사용한다. Vue에서의 상태 관리 패턴은 Vuex이다.    

## Vuex 설치하기
### NPM
```
npm install vuex --save
```
### Yarn
```
yarn add vuex
```

## Vuex 사용하기
설치 후, store 폴더의 index.js 파일에 다음과 같이 입력해 준다.

```
import Vue from 'vue';
import Vuex from 'vuex';

Vue.use(Vuex);

export default new Vuex.Store({
  state: {
    사용할 변수명: 값,
  },
  mutations: {
  },
  actions: {
  },
  modules: {
  },
});
```

변수를 사용할 vue 파일에서 사용하는 방법은 다음과 같다.
### template 태그 속 사용 방법
```
$store.state.변수명
```
### script 태그 속 사용 방법
```
this.$store.state.변수명
```

이렇게 상태 관리를 통해서 스크립트 안에서 변수의 값을 바꿀 수 있고, 템플릿 안에서는 변수의 값으로 검사를 하거나, 출력할 수 있다.
# Vue.js 기초🎇
vue 기초를 공부하며 정리해놓는 repository 입니다. 

 ### 목차
 1. [vue App 생성하기](#1장.-vue-app-생성하기)
 2. [template 문법](#2장.-vue의-template-문법-사용법)




## 1장. vue app 생성하기

 1.모든 vue project는 createApp 함수를 사용하여 새로운 앱 인스턴스를 생성하는 것으로 시작한다.<br />
 2. createApp 함수에 최상위 컴포넌트를 전달, mount method를 통해 랜더링한다. <br />
 3. mount에는 반드시 문자열로 인자를 전달한다.<br />
 ```ruby
 //main.js

import { createAPP } from "vue"
import App from './App.vue'

createApp(App).mount("#app")

```


## 2장. vue의 template 문법 사용법
 
 1. vue component의 구조
    - 

```ruby
<style></style>

<template></template>

<script></script>
```   
   

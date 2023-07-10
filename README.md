# Vue.js 기초🎇
vue 기초를 공부하며 정리해놓는 repository 입니다. 

<br />

 ## 🔸목차
 0. [알아야 할 개념/용어정리](#용어정리) 
 1. [vue App 생성하기](#1장-vue-app-생성하기)
 2. [vue의 template 문법 사용](#2장-vue의-template-문법-사용)

<br />
<br />

## 용어정리❗
 <br />
 
 1. v-directive
 vue에서 **HTML 태그 안에** v-접두사를 가지는 모든 속성들을 의미한다.<br />
 화면의 요소를 좀 더 쉽게 조작하기 위해 사용하는 기능이다.

`v-if, v-for, v-show, v-`

 <br />
 
 - **vue의 API 스타일**


vue component는 **options API**와 **Composition API** 두 가지 스타일로 작성할 수 있다. <br />
1. **Options API** <br />
option의 data,methods, mounted 같은 객체를 사용해서 컴포넌트 로직 정의. <br />
data에 반환된 속성들은 반응적인 상태가 되어 this에 노출된다.<br />
data는 데이터를 담고 있고, methods는 속성 값을 변경하고 업데이트 할 수 있으며 template 내에서 이벤트 리스너로 바인딩된다.<br /> mounted는 컴포넌트가 mount 된 후 호출된다.

```ruby

<script>
  export default{
  data(){
    return{
        conunt: 0
    }
  },

  methods:{
    increment(){
      this.count++
      },

    mounted(){
      console.log(`count:${this.count}`)
    }
  }
}
</script>

<template>
  <button v-on:click="increment">+</button>
</template>
```



1. **Composition API** <br />
import 해서 가져온 API 함수들은 사용하여 컴포넌트의 로직을 정의 <br />
코드를 기능별로 그룹화하고 재사용 가능한 로직을 작성하는 데 사용된다. <br />
composition API에 setup 옵션으로 데이터, 메서드, 생명주기 훅 등을 정의할 수 있다. <script setup> <br />
자동으로 런타임 코드를 생성하여 컴포넌트에 바인딩되기 때문에 따로 컴포넌트 옵션을 선언할 필요가 없다.<br />

```ruby

<script setup>
import { ref, onMouted } from 'vue' //import로 vue의 함수 가져와서 사용

const count = ref(0)  //ref 함루호 반응적인 상태의 count 변수 생성

function increment(){
 count.value++
}

onMounted(()=>{
 console.log(`count:${ count.value}`)
})

```

 
 <br />
 
- setup과 scoped<br />
**setup**은 vue3에서 도입되었으며, composition API를 사용할 때 적용되는 옵션이다. <br />
setup 블록 내에서는 import로 함수 가져오기, const, let으로 변수 선언하기, watch, watchEffec, onMounted 등의 생명주기 훅을 사용할 수 있음 <br />
**scoped** 는 vue의 <style> 블록에 적용되며, 사용할 시 컴포넌트의 범위로 스타일이 한정되어 다른 컴포넌트에 영향을 주지 않는다.
  
 
 <br />


## 1장 vue app 생성하기

 1.모든 vue project는 createApp 함수를 사용하여 새로운 앱 인스턴스를 생성하는 것으로 시작한다.<br />
 2. createApp 함수에 최상위 컴포넌트를 전달, mount method를 통해 랜더링한다. <br />
 3. mount에는 반드시 문자열로 인자를 전달한다.<br />
 ```ruby
 //main.js

import { createAPP } from "vue"
import App from './App.vue'

createApp(App).mount("#app")

```

<br />
<br />


## 2장 vue의 template 문법 사용
 
1. **vue component의 구조**
- vue의 템플릿 문법은 html기반이며, 데이터를 서술적으로 렌더링한 DOM에 데이터 바인딩을 할 수 있음
  

```ruby
<style></style> //css

<template> //html 
   <h1>{{title}}</h1> 
</template>

<script> 
 export default {
  data(){
     return{
       title : "데이터바인딩" 
   }   
  },
  method:{
 }
}
</script>
```
<br />




2. **vue component에서 데이터 바인딩**
   
2-1. __이중 중괄호__
- 가장 기본적인 형태는 이중 중괄호(Mustache)
- 동적인 데이터를 템플릿에 바인딩하고, 데이터가 변경되면 재랜더링 됨
- 중괄호 안에 데이터는 html이 아닌 일반 text로 해석된다
    
```ruby

<template>

  <h4>단순한 text 보관 : {{ text }}</h4> 

</template>

<script>

 export default{
  data(){
    return{
    const text : "객체 형태로 데이터를 할당"
  } 
 }
} 
 
</script>

```
<br />

2-2. __속성 바인딩__
- <> 태그 안에 데이터 바인딩 하고 싶을 때 기존의 {{}} 사용하지 않고 v-bind directive 사용
- v-bind는 자주 쓰이기 때문에 축약형으로 많이 씀

```ruby

<template>

  <div v-bind:id="idName1">속성 바인딩</div>  //directive는 v-  접두사를 가진 속성들

//축약형
  <div:id="idName2">속성 바인딩</div>  

</template>

<script>

 export default{
  data(){
    return{
    const idName1 = "container1"
    const idName2 = "container2"
  } 
 }
} 
 
</script>

```
<br />

2-3. __v-html directive로 바인딩__


```ruby

<template>

  <h4>Html 태그 바인딩 해보기 <span v-html="rawHtml"></span></h4>  

</template>

<script>

 export default{
  data(){
    return{
    const rawHtml = `<strong>html 태그를 바인딩했다!!</strong>`
  } 
 }
} 
 
</script>

```


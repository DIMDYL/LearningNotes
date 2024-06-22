##  好处

去掉了vuex中modules的概念，每一个store都是一个独立的模块

##  语法

组合式API写法，在里面定义的方法就是一个 actions 同步或异步修改数据的方法

computed：计算属性进行数据的过滤

``` js
import { ref, computed } from 'vue'
import { defineStore } from 'pinia'

export const useCounterStore = defineStore('counter', () => {
  const count = ref(0)
  const doubleCount = computed(() => count.value * 2)
  function increment() {
    count.value++
  }
  return { count, doubleCount, increment }
})
------------------------------
<script setup>
import { ref } from "vue";
import Son1 from "./components/Son1.vue";
import Son2 from "./components/Son2.vue";
import  { demo } from "@/stores/demo"
const demod = demo()
 const count = ref(10);
 const ad = () =>{
  demod.jia()
 } 
</script>
<template>
  {{ demod.count |  demod.up}}
  <button @click="ad">点击+1</button>
  <Son1></Son1>
  <Son2></Son2>
</template>
```

## storeToRefs

如果想要解构需要使用storeToRefs，才能让数据依然是响应式的

解构方法可以直接解构

``` vue
<script setup>
import { ref } from "vue";
import { storeToRefs } from "pinia";
import Son1 from "./components/Son1.vue";
import Son2 from "./components/Son2.vue";
import  { demo } from "@/stores/demo";
const demod = demo();
const { count, up } = storeToRefs(demod)
const { jia } = demod
 const ad = () =>{
  jia()
 }
</script>
<template>
  {{ count | up }}
  <button @click="ad">点击+1</button>
  <Son1></Son1>
  <Son2></Son2>
</template>
```

## 持久化插件

安装

``` linux
npm i pinia-plugin-persistedstate
```

## 配置

``` js
import './assets/main.css'
import { createApp } from 'vue'
import { createPinia } from 'pinia'
import App from './App.vue'
import piniaPluginPersistedstate from 'pinia-plugin-persistedstate'
const pinia = createPinia()

const app = createApp(App)
pinia.use(piniaPluginPersistedstate)

app.use(pinia)

app.mount('#app')
```

## 开启模块持久

persist: true持久化存储

``` js
import { defineStore } from 'pinia'
import { ref,computed } from 'vue'
export const demo = defineStore('counter', () => {
    const count = ref(100)
    function jia(){
        count.value++
    }
    const up = computed(()=>{
        return count.value+10
    })
    return{count, jia, up}
},{
    persist: true
})
```

#### 自定义配置

key：设置存储名称

storage：存储模式，默认是本地空间存储

paths：指定数据做持久化

``` js
import { defineStore } from 'pinia'
import { ref,computed } from 'vue'
export const demo = defineStore('counter', () => {
    const count = ref(100)
    function jia(){
        count.value++
    }
    const up = computed(()=>{
        return count.value+10
    })
    return{count, jia, up}
},{
    persist:{
        key: "DIM",
        storage: sessionStorage,
        paths: ['count'],
    }
})
```




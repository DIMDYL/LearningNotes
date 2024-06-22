## 配置pinia

``` js
import App from './App'
// #ifndef VUE3
import Vue from 'vue'
import './uni.promisify.adaptor'
Vue.config.productionTip = false
App.mpType = 'app'
const app = new Vue({
  ...App
})
app.$mount()
// #endif

// #ifdef VUE3
import { createSSRApp } from 'vue'
import { createPinia } from 'pinia' // pinia
import piniaPluginPersistedstate from 'pinia-plugin-persistedstate' // 持久化
export function createApp() {
  const app = createSSRApp(App)
  const pinia = createPinia()
  app.use(pinia) // 注册pinna
  pinia.use(piniaPluginPersistedstate) // 注册持久化
  return {
    app
  }
}
// #endif
```

## 配置模块

persist：自定义配置

storage：开启持久化

在uniapp中如果想要使用pinia持久化的话，不能直接使用storage:true来开启

需要提供get和set方法才行微信端不能写入localStorage，需要使用微信的方法来代替

``` js
import { ref, computed } from 'vue'
import { defineStore } from 'pinia'

export const useCounterStore = defineStore('counter', () => {
  const count = ref(100)
  const doubleCount = computed(() => count.value * 2)
  function increment() {
    count.value++
  }
  return { count, doubleCount, increment }
}, {
	persist: {
		storage:{
			getItem(key) {
				return uni.getStorageSync(key);
			},
			setItem(key, val) {
				return uni.setStorageSync(key, val);
			}
		}
	}
})

```


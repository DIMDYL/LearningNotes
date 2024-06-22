## 概述

vuex是一个vue的数据管理工具，用于管理vue通用的数据（多组件共享的数据）

## 场景

某个数据在很多个组件来使用

多个组件共同维护同一份数据

## 优势

共同维护一份数据，数据集中化观念里

响应式变化

操作简洁

## 创建一个空仓库

在vue-cli中创建项目的时候勾选了vuex就会自动配置好

``` js
// 引入vuex核心代码
import Vue from 'vue'
import Vuex from 'vuex'
// 插件安装
Vue.use(Vuex)
// 导出main.js使用(空仓库)
export default new Vuex.Store({
  state: {
  },
  getters: {
  },
  mutations: {
  },
  actions: {
  },
  modules: {
  }
})
---------- main.js -------------
import store from './store'
new Vue({
  store
}).$mount('#app')
```

## 添加数据

state提供唯一的公共数据源，所有共享的数据都要放在 store中的state中存储，类似于vue的data

``` js
export default new Vuex.Store({
  state: {
    count: 1
  }
})
```

## 获取数据

#### 为什么要将数据放入在计算函数中?

响应式更新

代码的复用性

逻辑清晰

#### 使用数据有两种方式

##### 通过引入store访问

``` js
export default {
  name: 'DimDyl',
  computed: {
    count () {
       return this.$store.state.count
    }
  }
}
--------------------------
import store from '@/store'
export default {
  name: 'DimDyl',
  computed: {
    count () {
      return store.state.count
    }
  }
}
```

## mapState：获取数据辅助函数

mapState是vuex提供的辅助函数，用于便捷的从vuex的state中映射到computed属性中

在computed引入就相当于是将 this.$store.state.count 放入computed中

``` js
import { mapState } from 'vuex'
export default {
  name: 'DimDyl',
  computed: {
    ...mapState(['count'])
  }
}

=
computed: {
    count () {
        return this.$store.state.count
    }
}
```

## mutations：修改数据

mutations是同步的

通过mutations来修改数据，state数据只能通过mutations来修改

vuex 遵循单项数据流，组件中不能直接修改仓库的数据

通过 strict: true 可以开启严格模式

``` js
export default new Vuex.Store({
  strict: true,
  state: {
    count: 1
  }
})
```

#### 修改数据

在mutations中定义修改state数据的方法

使用this.$store.commit('使用的方法名')来提交修改

``` js
export default new Vuex.Store({
  state: {
    count: 1
  },
  getters: {
  },
  mutations: {
    addCount (state) {
      state.count += 1
    },
    rmCount (state) {
      state.count -= 1
    }
  }
})
--------------------
add () {
  this.$store.commit('addCount')
}
```

#### 传参语法

传参只需要在mutations定义时，添加变量，只需要存储一个参数

如果必须要传多个参数，可以使用数组或者对象来接收

在提交的时候也要填写属性

``` js
export default new Vuex.Store({
  state: {
    count: 1
  },
  getters: {
  },
  mutations: {
    addCount (state, val) {
      state.count += val
    },
    rmCount (state, val) {
      state.count -= val
    }
  }
})
------------------
this.$store.commit('addCount', 10)
```

##  映射方法 辅助函数

mapMutations和mutations使用方法基本一致，都是用于映射的，一个是映射数据，一个是映射方法

``` js
mutations: {
    updateCount (state, val) {
      state.count = val
    }
}
-------------------
import { mapMutations } from 'vuex'
export default {
  methods: {
    ...mapMutations(['updateCount']),
    get (e) {
      console.log(e.target.value)
      this.updateCount(e.target.value)
    }
  }
  = 
updateCount (state, val) {
  state.count = val
}
```

## actions 处理异步操作

用于处理异步

通过 import { mapActions } from 'vuex'  可以便捷的使用异步处理函数

``` js
mutations: {
    updateCount (state, val) {
      state.count = val
    }
},
-----------------
export default new Vuex.Store({
  state: {
    count: 1
  },
  mutations: {
    setCount (state, val) {
      state.count = val
    }
  },
  actions: {
    setSyncCoumt (context, number) {
      setTimeout(() => {
        context.commit('setCount', number)
      }, 1000)
    }
  }
```

## mapActions：异步处理辅助函数

``` js
import { mapActions } from 'vuex'
  methods: {
    ...mapActions(['setSyncCoumt']),
    get (e) {
      this.setSyncCoumt(e.target.value)
    }
  }
=
setSyncCoumt (context, number) {
  setTimeout(() => {
    context.commit('setCount', number)
  }, 1000)
}
```


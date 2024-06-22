## provide和inject

使用provide和inject可以实现跨层级组件传递数据

例如：有三个组件 x1 x2 x3 如果x1想要给x3数据就可以使用provide和inject

```vue
<script setup>
provide('d1',100)
</script>
----------------------
<script setup>
const d1 = inject('d1')
</script>
```

## 如果想要在孙组件中修改接收的数据

遵循谁的数据就给来修改的原则，所以给孙组件传递一个修改数据的函数

``` vue
<script setup>
import { reactive } from 'vue';
const state = reactive({
  count: 1
});
const add = () => {
  state.count++
}
//传递一个修改数据的方法
provide('d1',add)
</script>
```

##  defineModel新特性

在传值的时候不使用props接收，直接使用defineModel来接收数据，数据是可以修改的

``` vue
<script setup>
import {  ref,onMounted, provide, inject } from 'vue';
import DDDD from './components/demo01/Son.vue';
const val = ref(100)
</script>
<template>
    <DDDD v-model="val"></DDDD>
    {{ val }}
</template>
-------------------------------
<script setup>
import { ref,defineModel } from 'vue';
const val = defineModel()
</script>
<template>
    <input 
    :value="val"
    @input="e=>val = e.target.value"
    >
</template>
-------------------
vue({
  script: {
    defineModel: true
  }
})
```


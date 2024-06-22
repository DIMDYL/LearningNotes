## computed

计算属性，于methods对比，computed会将计算的数据进行缓存，只有依赖项变了才会重新计算，并再次缓存

``` vue
computed: {
    dim () {
      console.log(1)
      return Number(this.a) + Number(this.b)
    }
 }
```

#### 完整使用方法

在computed中的计算中使用get和set，将获取和设置值分开

在修改值的地方，直接使用 计算类 = xxx的形式，这样这个计算类的set方法就会接收到值

``` vue
<template>
  <div class="index">
    <input type="text" v-model="firstname"> +  <input type="text" v-model="lastname">
    {{ dim }}
    <input type="button" @click="setname" value="改名">
  </div>
</template>

<script>
export default {
  data () {
    return {
      sum: 0,
      firstname: '邓',
      lastname: '安然'
    }
  },
  methods: {
    setname () {
      this.dim = '邓云龙'
    }
  },
  computed: {
    dim: {
      get () {
        return this.firstname + this.lastname
      },
      set (val) {
        this.firstname = val.slice(0, 1)
        this.lastname = val.slice(1)
      }
    }
  }
}
</script>

<style lang="less" scoped>

</style>
```


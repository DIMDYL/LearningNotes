## sync

.sync 修饰符可以用于自动绑定父组件与子组件之间数据的更新。

当一个子组件改变了一个父组件绑定的prop属性时，我们可以通过在子组件中显式地触发一个事件来通知父组件进行更新。

:size.sync="size" = @update:size = "size = $event"

``` vue
<NavTop page="1" :size.sync="size" pagesize="10" total="10"></NavTop>
--------------------
handleCurrentChange (size) {
  this.$emit('update:size', size)
}
```


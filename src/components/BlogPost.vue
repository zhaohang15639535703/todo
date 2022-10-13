<template>
<h2>{{normalizedTitle}}</h2>
<!--  插槽作为一个占位符-->
  <slot></slot>
  <button @click="$emit('enlarge-text')">Enlarge Text</button>
  <button @click="$emit('minify-text')">Minify Text</button>
</template>

<script>
export default {
  //所有的 props 都遵循着单向绑定原则，props 因父组件的更新而变化，
  // 自然地将新的状态向下流往子组件，而不会逆向传递。
  // 这避免了子组件意外修改父组件的状态的情况，
  // 不然应用的数据流将很容易变得混乱而难以理解。
  // 每次父组件更新后，所有的子组件中的 props 都会被更新到最新值，
  // 这意味着你不应该在子组件中去更改一个 prop
  name: "BlogPost",
  //props更改场景
  //1.prop被用于传入初始值，而子组件想在之后将其作为一个局部数据属性
  //解决方案：新定义一个局部数据属性，从props上获取初始值即可
  //2.需要对传入的props做进一步的转换，这种情况最好是基于该prop值定义一个计算属性
  //解决方案：使用计算属性computed:

  //更改对象/数组类型的props
  //当对象或数组作为 props 被传入时，虽然子组件无法更改 props 绑定，
  // 但仍然可以更改对象或数组内部的值。
  // 这是因为 JavaScript 的对象和数组是按引用传递，而对 Vue 来说，
  // 禁止这样的改动虽然可能，但有很大的性能损耗，比较得不偿失
  props: {
    title: String,
    num: Number,
    isPublished: Boolean,
    commentIds: Array,
    author: Object,
  },
  emits: ['enlarge-text','minify-text'],
  data(){
    return {
      counter: this.num //计数器只是将this.num作为初始值，
      // 后续的更新就与props无关了
    }
  },
  computed:{
    //该prop变更时计算属性也会自动更新
    normalizedTitle(){
      return this.title.trim().toLocaleLowerCase()
    }
  },
}
</script>

<style scoped>

</style>
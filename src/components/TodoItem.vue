<template>
<li>{{title}}
  <button @click="$emit('remove')" id="removeBtn">Remove</button>
  <label for="removeBtn">{{greetingMessage}}</label>
</li>
</template>

<script>
export default {
  name: "TodoItem.vue",
  // props: ['title'],
  props: {
    title: String,
    greetingMessage: String
    //如果一个prop的名字很长，
    // 应该使用camelCase的形式，因为他们是合法的JavaScript标识符
    //可以直接在模板表达式中使用，也可以避免在作为属性key时必须加上引号
  },
  emits: ['remove']
}
</script>

<style scoped>

</style>
<template>
<h4>{{propA}}</h4>
</template>

<script>
class Person {
  constructor(firstName, lastName) {
    this.firstName = firstName
    this.lastName = lastName
  }
}
export default {
  name: "PropsValidator",
  props: {
    //<!-- 等同于传入 :disabled="true" -->
    // <MyComponent disabled />
    // <!-- 等同于传入 :disabled="false" -->
    // <MyComponent />
    disabled: Boolean,
    author: Person,
    //props校验
    // 基础类型检查
    //（给出 `null` 和 `undefined` 值则会跳过任何类型检查）
    propA: Number,
    // 多种可能的类型，可以为String,也可以为Number
    propB: [String, Number],
    // 必传，且为 String 类型
    propC: {
      type: String,
      required: true
    },
    // Number 类型的默认值
    propD: {
      type: Number,
      default: 100
    },
    // 对象类型的默认值
    propE: {
      type: Object,
      // 对象或者数组应当用工厂函数返回。
      // 工厂函数会收到组件所接收的原始 props作为参数
      // eslint-disable-next-line no-unused-vars
      default(rawProps) {
        return { message: 'hello' }
      }
    },
    // 自定义类型校验函数
    propF: {
      validator(value) {
        // The value must match one of these strings
        return ['success', 'warning', 'danger'].includes(value)
      }
    },
    // 函数类型的默认值
    propG: {
      type: Function,
      // 不像对象或数组的默认，这不是一个工厂函数。这会是一个用来作为默认值的函数
      default() {
        return 'Default function'
      }
    }
  },
  //props细节:
  //1.所有 prop 默认都是可选的，除非声明了 required: true
  //2.除 Boolean 外的未传递的可选 prop 将会有一个默认值 undefined
  //3.Boolean 类型的未传递 prop 将被转换为 false。你应该为它设置一个 default 值来确保行为符合预期。
  //4.如果声明了 default 值，那么在 prop 的值被解析为 undefined 时，
  // 无论 prop 是未被传递还是显式指明的 undefined，都会改为 default 值
  //5.注意 prop 的校验是在组件实例被创建之前，所以实例的属性 (比如 data、computed 等)
  // 将在 default 或 validator 函数中不可用。
}
</script>

<style scoped>

</style>
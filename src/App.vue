<template>
  <form v-on:submit.prevent="addNewTodo">
    <label for="new-todo">Add a todo</label>
    <input
        v-model="newTodoText"
        id="new-todo"
        placeholder="E.g. Feed the cat"
    />
    <button>Add</button>
  </form>
  <ul>
<!--    todo-item与TodoItem相同-->
<!--    greeting-message与greetingMessage-->
    <todo-item
        v-for="(todo, index) in todos"
        :key="todo.id"
        :title="todo.title"

        greetingMessage="click this label to remove"
        @remove="todos.splice(index, 1)"
    ></todo-item>
  </ul>
<!--  传递不同的值类型-->
  <div class="mydiv" :style="{fontSize:blogFontSize+'px'}">
<!--    虽然42是一个常量，但还是要用v-bind，因为这是一个javascript表达式而不是字符串
,其它常量同理，比如Boolean,Array,Object等-->
  <BlogPost title="BlogPost" :num="blogFontSize" :author="{
    name: 'Veronica',
    company: 'Veridian Dynamics'
            }"
            :test-num="42" :is-published="false" :comment-ids="[22,22,33]"
            @enlarge-text="blogFontSize++" @minify-text="blogFontSize--">
    the font size is {{blogFontSize}}
  </BlogPost>
  </div>
  <div :style="{backgroundColor: 'pink',fontSize:blogFontSize+'px'}">
<!--        title: String,
    num: Number,
    isPublished: Boolean,
    commentIds: Array,
    author: Object,-->
<!--    绑定多个props这里等价于<BlogPost :title=post.title :isPublished=post.title :commentIds=post.commentIds :author=post.author>-->
    <BlogPost v-bind="post" @enlarge-text="blogFontSize++" @minify-text="blogFontSize--">
      the author is {{post.author}}
    </BlogPost>
    <input type="text" v-model="post.title">
  </div>
</template>

<script>
import TodoItem from './components/TodoItem.vue'
import BlogPost from "@/components/BlogPost"
import PropsValidator from "@/components/PropsValidator";

export default {
  name: 'App',
  components: {
    // eslint-disable-next-line vue/no-unused-components
    TodoItem,BlogPost,PropsValidator
  },
  data() {
    return {
      post:{
        title: 'Multiply Props',
        num: 1,
        isPublished: false,
        commentIds: [1,2,3],
        author: {
          name: 'zhaohang',
          qq: '731005515'
        },
      },
      blogFontSize: 20,
      newTodoText: '',
      todos: [
        {
          id: 1,
          title: 'Do the dishes'
        },
        {
          id: 2,
          title: 'Take out the trash'
        },
        {
          id: 3,
          title: 'Mow the lawn'
        }
      ],
      nextTodoId: 4
    }
  },
  methods: {
    addNewTodo() {
      this.todos.push({
        id: this.nextTodoId++,
        title: this.newTodoText
      })
      this.newTodoText = ''
    }
  }
}
</script>

<style scoped>
.mydiv{
  background-color: pink;
}

</style>
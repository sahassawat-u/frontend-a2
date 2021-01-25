<template>
<div>
    <section class="todoapp">
        <header class="header">
            <h1>{{ title }}</h1>
            <input class="new-todo" placeholder="What needs to be done?" 
            type='text' @keyup.enter="createTodo"
            autofocus>
        </header>
        <tasks :tasks="todos"/>
        <todo-footer 
          :activeTodoCount = 'activeTodos.length'
          @clear-todos = 'clearCompleted'
          :completedTodoCount = 'completedTodos.length'
        />
    </section>
    <footer class="info">
        <p>Double-click to edit a todo</p>
        <p>Created by <a href="http://todomvc.com">Sahassawat</a></p>
        <p>Part of <a href="http://todomvc.com">TodoMVC</a></p>
    </footer>
</div>
</template>


<script>
import Tasks from "./Task.vue";
import TodoFooter from './TodoFooter.vue'
export default {
  components:{
    Tasks, 
    TodoFooter
  },
  name: 'todo',
  data() {
      return {
        title: 'TO DO APP',
        todos: [ 
      { text: 'Learn JavaScript ES6+ goodies', isDone: false },
      { text: 'Learn Vue', isDone: false },
      { text: 'Build something awesome', isDone: false },
    ],
    editing: null,
      }
  },
  methods:{
    createTodo(event){
      const textbox = event.target;
      this.todos.push({
        text:textbox.value, isDone:false
      });
      textbox.value = '';
    },
    clearCompleted(){
      this.todos = this.activeTodos;
    },
  },
  computed:{
    activeTodos(){
      return this.todos.filter(t=>!t.isDone);
    },
    completedTodos(){
      return this.todos.filter(t=>t.isDone)
    }
  },
}
</script>
<template>
    <section class="main">
        <input id="toggle-all" class="toggle-all" type="checkbox">
        <label for="toggle-all">Mark all as complete</label>
        <ul class="todo-list">
            <li v-for="todo in tasks" :key="todo.id" 
            :class='{completed: todo.isDone, editing: todo === editing}'>
                <div class="view">
                <input class="toggle" type="checkbox" v-model="todo.isDone">
                <label @dblclick='startEditing(todo)'>{{todo.text}}</label>
                <button class="destroy" @click="destroyTodo(todo)"></button>
                </div>  
                <input class="edit" 
                    @keyup.esc="cancelEditing"
                    @keyup.enter="finishEditing"
                    @blur="finishEditing"
                    :value='todo.text'
                >
            </li>
        </ul>
    </section>
</template>

<script>
export default {
    props: ['tasks'],
    data() {
      return {
        editing: null,
      }
  },
    methods:{

    startEditing(todo){
      this.editing = todo;
    },
    finishEditing(event) {
      if (!this.editing) { return; }
      const textbox = event.target;
      this.editing.text = textbox.value;
      this.editing = null;
    },
    cancelEditing() {
      this.editing = null;
    },
    destroyTodo(todo){
      const index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    
  },
}
</script>
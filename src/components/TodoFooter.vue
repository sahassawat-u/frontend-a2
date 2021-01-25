<template>
    <footer class="footer">
        <span class="todo-count"><strong>{{activeTodoCount}}</strong> item left</span>
        <button class="clear-completed" 
        @click="$emit('clear-todos')" 
        v-show="completedTodoCount">Clear completed</button>
    </footer>
</template>

<script>
export default {
    props:{
        activeTodoCount:{
            type: Number,
            required: true,
        },
        completedTodoCount:{
            type: Number,
            required: true,
        }
    }
}
</script>
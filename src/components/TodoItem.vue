<template>
    <div class="todo-list" v-bind:class="{'complete':todo.completed}">
        <p>
            <input type="checkbox" v-on:change="markComplete">
            {{todo.title}}
            <button @click="$emit('del-todo', todo.id)" class="delete">X</button>
        </p>
    </div>
</template>

<script>
export default {
    name: "TodoItem",
    props:["todo"],
    methods: {
        markComplete(){
            this.todo.completed = !this.todo.completed;
        }
    }
}

</script>

<style scoped>
    .todo-list {
        background: #f4f4f4;
        padding: 10px;
        border-bottom: 1px #ccc dotted;
    }

    .complete {
        text-decoration: line-through;
    }

    .delete {
        background: #ff0000;
        color: #fff;
        border: none;
        padding: 5px 9px;
        border-radius: 50%;
        cursor: pointer;
        float: right;
    }
</style>
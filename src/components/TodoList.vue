<script setup>
import { ref } from 'vue'

const props = defineProps(['todoList'])

function isBlank(str) {
	return str.trim().length() == 0
}

function addTodo(todoListId) {
	const {lastId, input, todos} = props.todoList
    const todo = {id: lastId + 1, desc: input, done: false}
    todos.push(todo)		
    props.todoList.lastId++
    props.todoList.input = ''
}

function deleteTodo(todoId) {
    props.todoList.todos = props.todoList.todos.filter(({id}) => id != todoId)
}

function toggleExpanded() {
    props.todoList.expanded = !props.todoList.expanded
}
</script>

<template>
<li @click="toggleExpanded" class="todoList"> 
    {{ todoList.name }}({{ todoList.todos.length }})
    <ul v-if="todoList.expanded">
        <input 
          v-model="todoList.input"
          type="text"
          @click.stop
          @keyup.enter="addTodo"
        > 
        <button @click.stop="addTodo"> Add </button>
        <li class="todo" 
            v-for="todo in todoList.todos"
            @click.stop
        >
            <input 
              type="checkbox" 
              v-model="todo.done"
              @click.stop
            > 
            <span :class="{done: todo.done}"> {{ todo.desc }} </span>
        </li>
    </ul>
</li>
</template>

<style scoped>
 input[type=text] {
    padding: 5px; 
 }

 .todo {
    padding: 10px;
    padding-left: 0px;
 }

 .done {
    text-decoration: line-through;
 }

 .todoList {
    margin-bottom: 12px;
    padding: 20px;
    border: 1px solid black; 
 }


 ul {
    list-style-type: none;
    padding: 0px;
 }

 button {
    padding: 5px;
    margin-left: 5px;
 }
</style>

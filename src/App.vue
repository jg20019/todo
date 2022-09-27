<script setup>
import { reactive, ref } from 'vue'
import DateTimeBar from './components/DateTimeBar.vue'
import TodoList from './components/TodoList.vue'

const lastId = ref(0)
const chores = [
 {id: 1, desc: 'cut grass', done: false},
 {id: 2, desc: 'do laundry', done: false}
]

const todoLists = reactive([
 {id: lastId.value++, name: 'work', input: '', todos: [], expanded: true, lastId: 0},
 {id: lastId.value++, name: 'chores', input: '', todos: chores.slice(), expanded: false, lastId: 2}
])



</script>

<template>
    <DateTimeBar />
    <ul>
      <TodoList 
        v-for="list in todoLists" 
        :todoList="list"
        :lastId="lastId"
      />
    </ul>
</template>

<style scoped>
 ul {
    list-style-type: none;
    padding: 0px;
 }
</style>

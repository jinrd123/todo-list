<script setup>
import {ref} from "vue";
const todo = ref("");
const todoList = ref([]);
const addTodo = () => {
  todoList.value.push({todoName: todo.value, status: false});
  todo.value = "";
}
const deleteTodo = () => {
  todoList.value = todoList.value.filter((todo) => {
    return todo.status !== true;
  })
}
const finishTodo = (index) => {
  todoList.value[index].status = !todoList.value[index].status;
}
</script>

<template>
  <div>
    <input type="text" v-model="todo">
    <button @click="addTodo">add todo</button>
  </div>
  <ul>
    <li 
      v-for="todo, index in todoList" 
      :key="index"
      :style="{
        textDecoration: todo.status? 'line-through' : 'none'
      }"
    >
      {{ todo.todoName }}
      <button @click=finishTodo(index)>done</button>
    </li>
  </ul>
  <button @click="deleteTodo">delete finished todos</button>
</template>

<style scoped>

</style>

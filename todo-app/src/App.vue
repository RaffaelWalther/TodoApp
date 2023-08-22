<script setup lang="ts">
  import { ref } from 'vue';

  interface TodoItem {
    name : string
    checked : boolean
  }

  const todoName = ref("")
  const todos = ref<TodoItem[]>([]);

  function OnEnter() {
    todos.value.push({ name : todoName.value, checked : false });
    todoName.value = "";
  }

  function OnDelete(index : number){
    todos.value.splice(index, 1);
  }

</script>

<template>
  <h1>todos</h1>
  <input v-model="todoName" @keyup.enter="OnEnter" />
  <ul>
    <li v-for="(todo, index) in todos" :key="todo.name">
      <input type="checkbox" v-model="todo.checked" />
      <span :class="{checked : todo.checked}" >{{ todo.name }}</span>
      <button @click.stop.prevent="OnDelete(index)">x</button>
    </li>
  </ul>

</template>

<style scoped>
  .checked{
    text-decoration: line-through;
  }
</style>
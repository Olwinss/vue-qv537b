<template>
<div class="app">
  <h1>Todo List</h1>
  <form @submit.prevent="addTodo">
    <input type="text" v-model="nTitle" placeholder="Title" />
    <input type="text" v-model="nDescription" placeholder="Description" />
    <input type="date" v-model="nDate" />
    <button type="submit">Add</button>
  </form>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      <h2>{{ todo.title }}</h2>
      <p>{{ todo.description }}</p>
      <p>{{ todo.date }}</p>
      <p>{{ todo.status }}</p>
      <select @change="changeStatus(todo, $event)">
        <option value="A faire" :selected="todo.status === 'A faire'">A faire</option>
        <option value="En cours" :selected="todo.status === 'En cours'">En cours</option>
        <option value="Terminé" :selected="todo.status === 'Terminé'">Terminé</option>
      </select>
      <button @click="clearTodo(todo)">Clear</button>
    </li>
  </ul>
  <button @click="clearAll()">Clear</button>
</div>
</template>


<script setup>
import { ref } from 'vue';

const id = ref(0);
const nTitle = ref('');
const nDescription = ref('');
const nDate = ref('');
const todos = ref([]);

</script>



<script>
export default {
  name: 'TodoList',
  data() {
    return {
      id: 0,
      nTitle: '',
      nDescription: '',
      nDate: '',
      todos: [
        {
          id: 1,
          title: 'Todo 1',
          description: 'Description 1',
          date: '2021-10-10',
          status: 'A faire',
        },
        {
          id: 2,
          title: 'Todo 2',
          description: 'Description 2',
          date: '2021-10-11',
          status: 'A faire',
        },
      ],
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.id++,
        title: this.nTitle,
        description: this.nDescription,
        date: this.nDate,
        status: 'A faire', // You may want to set a default status here
      });
      this.nTitle = '';
      this.nDescription = '';
      this.nDate = '';
    },
    clearTodo(todo) {
      this.todos = this.todos.filter((t) => t.id !== todo.id);
    },
    clearAll() {
      this.todos = [];
    },

    changeStatus(todo, event) {
      todo.status = event.target.value;
    },
  },
};
</script>
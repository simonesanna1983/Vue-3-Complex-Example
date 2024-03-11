<script setup lang="ts">
import { ref, onMounted } from 'vue';
import Loading from '../shared/ui/Loading.vue';
import '../styles/body.css';

defineProps<{ msg: string }>();

const isTodosVisible = ref(true);
const showLoading = ref(false);

const todos = ref([]);
const users = ref([]);

function manageTodosVisibility() {
  isTodosVisible.value = !isTodosVisible.value;
}
function deleteTodo(id: number) {
  todos.value = todos.value.filter((x) => x.id !== id);
}

function fetchUsers() {
  showLoading.value = true;
  fetch('https://jsonplaceholder.typicode.com/users')
    .then((response) => response.json())
    .then((data) => {
      // Assign the fetched data to the todos array
      users.value = data;
      showLoading.value = false;
    })
    .catch((error) => {
      console.error('Error fetching data:', error);
      showLoading.value = false;
    });
}

onMounted(() => {
  showLoading.value = true;

  fetch('https://jsonplaceholder.typicode.com/todos')
    .then((response) => response.json())
    .then((data) => {
      // Assign the fetched data to the todos array
      todos.value = data.slice(0, 5);
      showLoading.value = false;
    })
    .catch((error) => {
      console.error('Error fetching data:', error);
      showLoading.value = false;
    });
});
</script>

<template>
  <div class="container-app">
    <Loading :show="showLoading" />
    <h1>{{ msg }}</h1>

    <div class="form-check form-switch" v-on:click="manageTodosVisibility">
      <input
        class="form-check-input"
        type="checkbox"
        id="flexSwitchCheckDefault"
        :checked="isTodosVisible"
      />
      <label class="form-check-label" for="flexSwitchCheckDefault"
        >Show/Hide Todos</label
      >
    </div>
    <br />

    <h1>Todos</h1>
    <ul v-if="isTodosVisible">
      <li v-for="todo in todos" :key="todo.id">
        {{ todo.title }}
        <span style="cursor: pointer" v-on:click="deleteTodo(todo.id)">❌</span>
      </li>
    </ul>
    <div v-if="todos.length === 0">no todos to show</div>

    <hr />

    <button v-on:click="fetchUsers">Load Users</button>

    <h1>Users</h1>
    <ul>
      <li v-for="user in users" :key="user.id">{{ user.name }}</li>
    </ul>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>

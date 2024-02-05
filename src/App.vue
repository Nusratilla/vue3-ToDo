

<template>
  <main class="app">
    <section class="greeting">
      <h2 class="title">
        Hello! <input type="text" placeholder="Name Here" v-model="name">
      </h2>
    </section>

    <section class="create-todo">
      <h3>Create A ToDo</h3>
      <form @submit.prevent="addTodo">
        <h4>Whats's on your todo list?</h4>
        <input type="text" placeholder="e.g. Study IT" v-model="input_content">
        <h4>Pick a category</h4>
        <div class="options">
          <label>
            <input type="radio" name="category" value="business" v-model="input_category" />
            <span class="bubble business"></span>
            <div>Business</div>
          </label>
          <label>
            <input type="radio" name="category" value="personal" v-model="input_category" />
            <span class="bubble personal"></span>
            <div>Personal</div>
          </label>
        </div>
      </form>
    </section>


  </main>
</template>

<script setup>
import { ref, onMounted, computed, watch } from 'vue'

const todos = ref([])
const name = ref('')

const input_content = ref('')
const input_category = ref(null)

const todos_asc = computed(() => todos.value.sort((a, b) => {
  return a.createdAt - b.createdAt
}))

watch(name, (newValue) => {
  localStorage.setItem('name', newValue)
})

onMounted(() => {
  name.value = localStorage.getItem('name') || ''
})
</script>


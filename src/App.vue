<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'

fetch('http://localhost:3000/todos')
  .then((response) => {
    console.log(response)
    return response.json()
  })
  .then((data) => {
    const todoElement = document.getElementById('todoContainer')

    todoElement.innerHTML = data
      .map(
        (todo) => `
      <div class="todo">
        <span>${todo.content}</span>
        <span class="done">${todo.done}</span>
        <span class="date">${todo.date}</span>  
      </div> 
    `,
      )
      .join('')
  })
  .catch((error) => {
    console.log(error)
  })
</script>

<template>
  <header>
    <div class="wrapper">
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/posts">Posts</RouterLink>
        <RouterLink to="/todos">Todos</RouterLink>
      </nav>
    </div>
  </header>

  <!-- TODO SKA INTE VA HÄR, FLYTTA TILL BÄTTRE PLATS -->
  <div id="todoContainer" class="todo-container"></div>
  <RouterView />
</template>

<style lang="scss">
.todo-container {
  background-color: rgb(209, 209, 209);
  margin: 1rem;
  padding: 1rem;
  border-radius: 1rem;
  gap: 1rem;
  display: flex;
  flex-direction: column;
}
</style>

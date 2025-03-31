<script setup lang="ts">
import { ref } from 'vue'

interface Todo {
  id: number
  content: string
  done: boolean
  date: string
}

const todoElement = ref<HTMLDivElement | null>(null) // Vue ref för att hantera DOM-element

const getQueryString = (e?: Event): string => {
  if (e) {
    const target = e.target as HTMLInputElement | HTMLSelectElement
    console.log(target.name, target.value)
    return `?${target.name}=${encodeURIComponent(target.value)}`
  }
  return ''
}

const fetchTodos = async (e?: Event): Promise<void> => {
  try {
    const response = await fetch('http://localhost:3000/todos' + getQueryString(e))

    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`)
    }

    const data: Todo[] = await response.json()
    console.log('Todos fetched:', data)

    const todoElement = document.getElementById('todoContainer') as HTMLDivElement | null

    if (!todoElement) {
      console.error("Element with ID 'todoContainer' not found.")
      return
    }

    todoElement.innerHTML = data
      .map(
        (todo) => `
        <div class="todo">
          <h3>${todo.content}</h3>
          <span class="done">${todo.done}</span>
          <span class="date">${todo.date}</span>
        </div>
      `,
      )
      .join('')
  } catch (error) {
    if (todoElement.value) {
      todoElement.value.innerHTML = 'Oops! Something went wrong. Please try again later.'
    }
    console.error('Fetch error:', error)
  }
}

fetchTodos()
</script>

<template>
  <main>
    <h1>Todos</h1>
    <form id="topSection">
      <input type="text" class="form-control" id="search" placeholder="Search" name="search" @input="fetchTodos" />
      <select class="form-select" id="sort" name="sort" @change="fetchTodos">
        <option value="">Sort</option>
        <option value="asc">Ascending</option>
        <option value="desc">Descending</option>
      </select>
    </form>
    <div id="todoContainer" ref="todoContainer" class="todo-container"></div>
  </main>
</template>

<style lang="scss" scoped>
main {
  background-color: rgb(203, 228, 208);
  margin: 1rem;
  padding: 1rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-content: center;
  border-radius: 1rem;
  box-shadow: 0px 12px 30px rgba(29, 29, 30, 0.224);
}
</style>

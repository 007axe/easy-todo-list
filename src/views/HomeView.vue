<script setup>
import { ref,reactive, onMounted } from 'vue'

const list =  reactive([])
const newTodo = ''


const addTodo = (newTodo) => {
  const todoData = {
    name: newTodo,
    status: 'Doing'
    }
    list.push(todoData)

  }
  const deleteTodo = (index) => {
    list.splice(index,1)
  } 
  const changeStatus = (event, index) => {
    if(event.target.checked) {
      list[index].status = 'Done'
      console.log(list[index].status)
    } else {
      list[index].status = 'Doing'
      console.log(list[index].status)
    }
  }
  
</script>

<template>
  <main class="w-full h-screen flex justify-center items-center">
    
    <div class="w-96 p-6 rounded-md shadow-[0_10px_20px_rgba(255,_255,_255,_0.7)]">
      <h1 class="text-center text-2xl font-bold mb-5">Todo-list</h1>
      <div class="flex justify-center">
        <input class="text-black rounded-md w-full" v-model="newTodo">
        <button 
        class="bg-green-500 hover:bg-green-900 py-1 px-2 rounded-md ml-2"
        @click="addTodo(newTodo)">
          Add
        </button>
      </div>
      <ul class="mt-4">
        <li class="mt-2" v-for="(todo, index) in list" :key="todo">
          <div class="flex justify-between ">
            <input type="checkbox" 
            @change="changeStatus($event, index)"
            >
            <p :class="todo.status === 'Done' ? 'text-green-500 line-through' : ''">
              {{ todo.name }}
            </p>
            <p>{{ todo.status }}</p>
            <button
            class="bg-red-500 hover:bg-red-900 py-1 px-2 rounded-md"
            @click="deleteTodo(index)">
              Delete
            </button>
          </div>
          <div class="w-full bg-white p-[0.5px] mt-2"></div>
        </li>
      </ul>
    </div>
  </main>
</template>

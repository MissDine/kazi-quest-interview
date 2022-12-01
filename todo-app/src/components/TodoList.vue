<template>
  <div class="h-full w-full">
    <div class="text-lg font-semibold">
      <todo-header></todo-header>
    </div>

    <div class="h-full w-11/12 md:w-9/12 mx-auto">
      <div class="w-full mx-auto text-sm flex justify-end">
        <div class="w-1/2 flex items-center mt-5 justify-end m-5">
          <div class="mx-1 font-semibold"><span>Filter</span></div>
          <div
            class="rounded px-3 py-1 text-white font-semibold inline-block"
            :class=" all_filter ? 'bg-green-400':'bg-gray-400 cursor-pointer'"
            @click="(e: MouseEvent) => { all_filter = true; return e;}"
          >
            <span>All</span>
          </div>
          <div
            class="rounded bg-green-400 px-3 py-1 text-white font-semibold inline-block mx-3"
            :class=" active_filter ? 'bg-green-400':'bg-gray-400 cursor-pointer'"
            @click="(e: MouseEvent) => { active_filter = true; return e;}"
          >
            <span>Active</span>
          </div>
          <div
            class="rounded bg-green-400 px-3 py-1 text-white font-semibold inline-block"
            :class=" complete_filter ? 'bg-green-400':'bg-gray-400 cursor-pointer'"
            @click="(e: MouseEvent) => { complete_filter = true; return e;}"
          >
            <span>Complete</span>
          </div>
        </div>
      </div>
      <div class="w-full px-5">
        <div class="w-full  flex justify-end">
            <div class="px-3 py-1 rounded bg-red-500 inline-block"
            @click="(e: MouseEvent) => { deleteCompleted(); return e;}">
                <span class="text-sm text-white font-semibold">Delete completed</span>
            </div>
        </div>
      </div>
      <div v-for="(todo, index) in todos" :key="index" class="m-5">
        <todo-task
        :todo="todo"
            :class="(complete_filter && todo.complete)? '':((active_filter && todo.active)? '':(all_filter ? '':'hidden'))"
          @toggle-complete="
            (n: string) => {
              toggleTaskAsComplete(n)
            }
          "
          @delete-todo="
            (n: string) => {
              deleteTodoFromList(n)
            }
          "
        ></todo-task>
      </div>
      <div>
        <add-todo
          @add-todo="
            (n: Todo) => {
              addToTheList(n)
            }
          "
          @delete-todo="
            (n: string) => {
              deleteTodoFromList(n)
            }
          "
        ></add-todo>
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
import { ref, watch } from 'vue'
import TodoHeader from './TodoHeader.vue'
import TodoTask from './TodoTask.vue'
import AddTodo from './AddTodo.vue'
import { Todo } from '../types'

const all_filter = ref(true)
const active_filter = ref(false)
const complete_filter = ref(false)

watch(all_filter, ()=>{
    if (all_filter.value){
        active_filter.value = false
        complete_filter.value = false
    }
})

watch(active_filter, ()=>{
    if (active_filter.value){
        all_filter.value = false
        complete_filter.value = false
    }
})

watch(complete_filter, ()=>{
    if (complete_filter.value) {
        all_filter.value = false
        active_filter.value = false
    }
})

const addToTheList = (todo: Todo) => {
  todos.value.push(todo)
}

const deleteTodoFromList = (id: string) => {
  let todos_left = todos.value.filter((todo) => todo.id != id)
  todos.value = todos_left
}

const toggleTaskAsComplete = (id: string) => {
  todos.value.forEach((todo) => {
    if (todo.id == id) {
      todo.active = !todo.active
      todo.complete = !todo.active
    }
  })
}

const deleteCompleted = () => {
    let todos_left = todos.value.filter((todo) => !todo.complete)
    todos.value = todos_left 
}

const todos = ref<Todo[]>([
  {
    id: '0',
    todo: 'Buy new laptop',
    description: 'Buy new laptop to facilitate developer life',
    active: false,
    complete: false
  },
  {
    id: '1',
    todo: 'Get feedback',
    description: 'Design responsive website in Vue for different layouts',
    active: false,
    complete: false
  },
  {
    id: '2',
    todo: 'About the trip',
    description: 'Call my friends about the trip',
    active: false,
    complete: false
  },
])
</script>
<style scoped></style>

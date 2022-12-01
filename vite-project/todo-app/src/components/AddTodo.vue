<template>
    <div class="m-5">
    <div class="font-semibold">
        <span>Add todo</span>
    </div>
    <div>
        <input class="h-10 p-1 border border-gray-300 outline-none rounded"
        v-model="todo_to_add"/>
    </div>
    <div class=" h-32 w-full">
        <textarea v-model="description_to_add" class="h-full w-full border border-gray-300 outline-none p-1 my-3 resize-none rounded"></textarea>
    </div>
    <div class="my-6">
        <div class="rounded px-4 py-2 text-white font-semibold inline-block w-3/12"
        :class="todo_to_add && description_to_add ? 'bg-green-400 cursor-pointer':'bg-gray-400'"
        @click="(e: MouseEvent) => { addTodo(); return e}">
            <div class="h-full w-full text-center">
                <span>Add</span>
            </div>
        </div>
    </div>
    </div>
</template>
<script setup lang="ts">
import { ref } from "vue";
import { v4 as uuidv4 } from 'uuid';

const emit = defineEmits(['addTodo'])

const todo_to_add = ref("")
const description_to_add = ref("")

const addTodo = () => {
    if (todo_to_add.value && description_to_add.value){
        emit('addTodo', { id: uuidv4(), todo: todo_to_add.value, description: description_to_add.value})
    }
}
</script>
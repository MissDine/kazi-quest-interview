<template>
    <div class=" text-black px-5 py-3 shadow h-full flex justify-center rounded bg-white">
        <div class="flex flex-col flex-1">
            <div class="font-semibold flex items-center my-2">
                <div class="rounded h-4 w-4 mr-3 cursor-pointer"
                :class=" todo.complete ? 'bg-green-500' : (todo.active?  'bg-orange-500':'bg-gray-100')"
                @click="$emit('toggleComplete', todo.id)">
                </div>
                <div>
                    <span>{{todo.todo}}</span>
                </div>
                <div class="mx-1 px-3 py-1 rounded text-sm"
                :class=" todo.complete ? 'bg-green-500' : (todo.active?  'bg-orange-500':'bg-gray-100')">
                    <span v-if="todo.complete">Complete</span>
                    <span v-else-if="todo.active">Active</span>
                    <span v-else>Inactive</span>
                </div>
            </div>
            <div class="text-sm font-thin">
                <span>{{todo.description}}</span>
            </div>
        </div>
        <div class="w-2/12 md:w-1/12 flex justify-end p-2">
            <div>
                <i class="fa fa-trash text-gray-600 cursor-pointer" aria-hidden="true"
                @click="$emit('deleteTodo', todo.id)"></i>
            </div>
        </div>
    </div>
</template>
<script setup lang="ts">
import { Todo } from "../types"

defineProps<{
    todo: Todo
}>()

</script>
<style scoped>
</style>
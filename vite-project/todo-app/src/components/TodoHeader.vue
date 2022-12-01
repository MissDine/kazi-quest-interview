<template>
    <div class="h-20 w-full flex flex-col justify-center p-5 shadow bg-white">
        <div>
            <div>
                <span>Todo App</span>
            </div>
            <div class="text-sm">
                {{dt.toLocaleString(DateTime.DATE_HUGE)}}
            </div>
        </div>
    </div>
</template>
<script setup lang="ts">
import { ref } from "vue";
import { DateTime } from "luxon";

const dt = ref(DateTime.now());
</script>
<style scoped></style>
<template>
    <div class="flex items-center space-x-2">
        <!-- <input
            type="number"
            name="hours"
            min="0"
            class="w-16 border border-gray-300 rounded-md shadow-sm focus:border-blue-500 focus:ring focus:ring-blue-200 focus:ring-opacity-50 p-2"
            placeholder="Часы"
        > -->
        <input
            type="number"
            name="minutes"
            min="0"
            max="1500"
            class="w-16 border border-gray-300 rounded-md shadow-sm focus:border-blue-500 focus:ring focus:ring-blue-200 focus:ring-opacity-50 p-2"
            placeholder="Минуты"
            v-model="duration"
        ><input
            type="text"
            name="taskName"
            required
            class="flex-1 border border-gray-300 rounded-md shadow-sm focus:border-blue-500 focus:ring focus:ring-blue-200 focus:ring-opacity-50 p-2"
            placeholder="Название задачи"
            v-model="name"
            @keyup.enter="addAction"
        >
        <button
            type="submit"
            class="bg-blue-500 text-white font-semibold py-2 px-4 rounded-md hover:bg-blue-600 focus:outline-none focus:ring-2 focus:ring-blue-400 focus:ring-opacity-50"
            @click="addAction"
        >+</button>
    </div>
</template>

<script lang="ts" setup>
import { Action } from '@/types/action';
import { ref } from 'vue';

const name = ref<String>("");
const duration = ref<Number>(20);

const emit = defineEmits({
    createAction(action: Action) { }
});

function addAction() {
    emit('createAction', {
        name: name.value,
        duration: duration.value,
    });
    name.value = "";
}

</script>
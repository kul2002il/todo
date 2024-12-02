<template>
    <div class="max-w-lg mx-auto mt-10 p-5 border rounded shadow-lg">
      <h1 class="text-2xl font-bold mb-4">Список дел</h1>
      <input
        v-model="newTodo"
        @keyup.enter="addTodo"
        class="border p-2 w-full mb-4"
        placeholder="Добавить новое дело"
      />
      <ul>
        <li
          v-for="(todo, index) in todos"
          :key="index"
          class="flex items-center justify-between mb-2"
        >
          <div class="flex items-center">
            <input
              type="checkbox"
              v-model="todo.completed"
              class="mr-2"
            />
            <span :class="{ 'line-through text-gray-400': todo.completed }">{{ todo.text }}</span>
          </div>
          <button
            @click="removeTodo(index)"
            class="bg-red-500 text-white px-2 py-1 rounded hover:bg-red-600"
          >
            Удалить
          </button>
        </li>
      </ul>
    </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue';

interface Todo {
  text: string;
  completed: boolean;
}

const newTodo = ref<string>('');
const todos = ref<Todo[]>([]);

const addTodo = () => {
    if (newTodo.value.trim()) {
    todos.value.push({ text: newTodo.value, completed: false });
    newTodo.value = '';
    }
};

const removeTodo = (index: number) => {
    todos.value.splice(index, 1);
};

</script>
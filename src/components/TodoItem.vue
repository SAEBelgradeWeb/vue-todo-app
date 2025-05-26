<script>
export default {
  name: 'TodoItemm',
  props: {
    todo: {
      type: Object,
      required: true
    },
  },
}
</script>

<template>
  <li class="bg-white rounded-sm py-2 px-3 text-sm text-neutral-800">
    <div class="flex justify-between">
      <div class="flex gap-2 flex-1 cursor-pointer" @click="todo.completed = !todo.completed">
        <input type="checkbox" v-model="todo.completed" />
        <span :class="todo.completed && 'line-through text-neutral-500'">{{ todo.title }}</span>
      </div>

      <button @click="$emit('deleteTodo', todo)"
              class="cursor-pointer text-red-500">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 20 20"
          fill="currentColor"
          class="size-5"
        >
          <path
            d="M6.28 5.22a.75.75 0 0 0-1.06 1.06L8.94 10l-3.72 3.72a.75.75 0 1 0 1.06 1.06L10 11.06l3.72 3.72a.75.75 0 1 0 1.06-1.06L11.06 10l3.72-3.72a.75.75 0 0 0-1.06-1.06L10 8.94 6.28 5.22Z"
          />
        </svg>
      </button>
    </div>
  </li>
</template>

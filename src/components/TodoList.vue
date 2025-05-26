<script>
import TodoItem from '@/components/TodoItem.vue'

export default {
  name: 'TodoList',
  components: { TodoItem },
  props: {
    todos: {
      type: Array,
      required: true
    }
  }
}
</script>

<template>
  <ul class="flex flex-col gap-4">
    <TodoItem
      v-for="(todo, index) in todos"
      :todo="todo"
      @delete-todo="(item) => $emit('deleteTodo', item)"
      :key="index"
    />
  </ul>
</template>

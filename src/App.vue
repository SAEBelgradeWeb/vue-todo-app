<script>
import TodoList from '@/components/TodoList.vue'
import TodoFilters from '@/components/TodoFilters.vue'

export default {
  components: {
    TodoList,
    TodoFilters
  },
  data() {
    return {
      newTodo: '',
      todos: [],
      currentFilter: 'all',
      filters: ['all', 'completed', 'active'],
    }
  },
  computed: {
    activeTodos() {
      return this.todos.filter((todo) => !todo.completed)
    },

    filteredTodos() {
      if (this.currentFilter === 'active') {
        return this.activeTodos
      }

      if (this.currentFilter === 'completed') {
        return this.completedTodos
      }

      return this.todos
    },

    completedTodos() {
      return this.todos.filter((todo) => todo.completed)
    },
  },
  methods: {
    addNewTodo() {
      if (!this.newTodo) return

      this.todos.push({
        title: this.newTodo,
        completed: false,
      })

      this.newTodo = ''
    },

    deleteTodo(todo) {
      let position = this.todos.indexOf(todo)

      this.todos.splice(position, 1)
    },

    clearCompleted() {
      this.todos = this.activeTodos
    },

    filterTodos(filter) {
      this.currentFilter = filter
    },
  },
}
</script>

<template>
  <div class="h-full grid place-content-center text-center">
    <h1 class="text-3xl font-bold">Vue Todo App</h1>

    <TodoFilters
      :state="currentFilter"
      @update-filter="(state) => currentFilter = state"
    />

<!--    <TodoFilters-->
<!--      :filters="filters"-->
<!--      :current="currentFilter"-->
<!--      @filter-todos="(filter) => filterTodos(filter)"-->
<!--    />-->

    <div class="mt-10">
      <input
        v-model="newTodo"
        @keyup.enter="addNewTodo"
        type="text"
        class="px-3 py-2 w-92 bg-white text-neutral-800 rounded-xl outline-none cursor-default"
        placeholder="What needs to be done?"
      />
    </div>

    <section class="mt-10 text-left">
      <TodoList
        :todos="filteredTodos"
        @delete-todo="(item) => deleteTodo(item)"
      />
    </section>

    <footer class="text-white mt-5">
      <hr class="text-neutral-500" />
      <div class="flex justify-between text-sm pt-2">
        <span>{{ activeTodos.length }} todos left</span>

        <button @click="clearCompleted" class="cursor-pointer hover:underline">
          Clear completed
        </button>
      </div>
    </footer>
  </div>
</template>

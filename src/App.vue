<script>
export default {
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
      if(this.currentFilter === 'active') {
        return this.activeTodos;
      }

      if(this.currentFilter === 'completed') {
        return this.completedTodos
      }

      return this.todos;
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

    <div class="flex gap-3 justify-center mt-5">
      <button
        v-for="(filter, index) in filters"
        :key="index"
        class="border px-2 text-base capitalize cursor-pointer"
        @click="filterTodos(filter)"
      >
        {{ filter }}
      </button>
    </div>

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
      <ul class="flex flex-col gap-4">
        <li
          v-for="(todo, index) in filteredTodos"
          :key="index"
          class="bg-white rounded-sm py-2 px-3 text-sm text-neutral-800"
        >
          <div class="flex justify-between">
            <div class="flex gap-2 flex-1 cursor-pointer" @click="todo.completed = !todo.completed">
              <input type="checkbox" v-model="todo.completed" />
              <span :class="todo.completed && 'line-through text-neutral-500'">{{
                todo.title
              }}</span>
            </div>

            <button @click="deleteTodo(todo)" class="cursor-pointer text-red-500">
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
      </ul>
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

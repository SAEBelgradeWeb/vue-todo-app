<script>
export default {
  name: 'TodoFilters',
  props: {
    state: {
      type: String,
      default: 'all'
    }
    // filters: Array,
    // current: String,
  }
}
</script>

<template>
  <input
    type="radio"
    :checked="state === 'all'"
    name="filter"
    value="all"
    @change="$emit('update-filter', $event.target.value)"
  >
  <input
    type="radio"
    :checked="state === 'completed'"
    name="filter"
    value="completed"
    @change="$emit('update-filter', $event.target.value)"
  >

  <input
    type="radio"
    name="filter"
    :checked="state === 'active'"
    value="active"
    @change="$emit('update-filter', $event.target.value)"
  >

  {{ state }}
<!--  <div class="flex gap-3 justify-center mt-5">-->
<!--    <button-->
<!--      v-for="(filter, index) in filters"-->
<!--      :key="index"-->
<!--      :class="filter === current && 'bg-white text-black'"-->
<!--      class="border px-2 text-base capitalize cursor-pointer"-->
<!--      @click="$emit('filterTodos', filter)"-->
<!--    >-->
<!--      {{ filter }}-->
<!--    </button>-->
<!--  </div>-->
</template>

<style scoped>

</style>

<template>
  <li :class="['todo-item', todo.completed?'completed':'']"
    @mouseover="showClearBtn=true"
    @mouseout="showClearBtn=false">
    <label class="text">
      <input class="toggle"
        type="checkbox"
        v-model="todo.completed"
        @click="$emit('toggle', todo)">
      {{ todo.text }}
    </label>
    <button :class="['clear', showClearBtn?'':'hide']"
      @click="$emit('clear', todo.id)">
      x
    </button>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      showClearBtn: false
    }
  }
}
</script>

<style scoped>
  .todo-item {
    display: flex;
    justify-content: space-between;
    font-size: 24px;
    color: #555;
    padding: 10px 0;
    border-bottom: 1px solid #ccc;
  }

  .completed {
    text-decoration: line-through;
    color: #d9d9d9;
  }
  .clear {
    cursor: pointer;
    border: none;
    outline: none;
    background: transparent;
    font-size: 24px;
    color: #999;
  }

  .clear:hover {
    color: #555;
  }

  .hide {
    display: none;
  }
</style>

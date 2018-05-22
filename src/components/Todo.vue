<template>
  <div class="todo">
    <input
      type="text"
      class="newTodo"
      autofocus
      placeholder="What needs to be done?"
      v-model="newTodoText"
      @keyup.enter="addTodo">
    <ul>
      <input type="checkbox"
        v-if="todos.length"
        v-model="allDone"
        class="toggle-all">
      <TodoItem
      v-for="todo in filteredTodos"
      :key="todo.id"
      :todo="todo"
      v-model="todo.completed"
      @clear="clearTodo"
      @toggle="toggleTodo"/>
    </ul>
    <TodoTabs v-if="todos.length"
      @filter="toggleFilter"
      @clearCompleted="clearCompleted"
      :remaining="remaining"
      :visibility="visibility"/>
  </div>
</template>

<script>
import TodoItem from './TodoItem.vue'
import TodoTabs from './TodoTabs.vue'

const filters = {
  all(todos) {
    return todos
  },
  active(todos) {
    return todos.filter(item => !item.completed)
  },
  completed(todos) {
    return todos.filter(item => item.completed)
  }
}
export default {
  components: {
    TodoItem,
    TodoTabs,
  },
  data() {
    return {
      nextTodoId: 1,
      newTodoText: '',
      todos: [],
      visibility: 'all'
    }
  },
  computed: {
    filteredTodos() {
      return filters[this.visibility](this.todos)
    },
    remaining() {
      return this.todos.filter(item => !item.completed).length
    },
    allDone: {
      get() {
        return this.remaining === 0
      },
      set(value) {
        this.todos.forEach(item => item.completed = value)
      }
    }
  },
  
  methods: {
    addTodo() {
      const trimmedText = this.newTodoText.trim()
      if (trimmedText) {
        this.todos.unshift({
          id: this.nextTodoId++,
          text: trimmedText,
          completed: false
        })
        console.log(this.todos)
        this.newTodoText = ''
      }
    },
    toggleTodo(todo) {
      todo.completed = !todo.completed
    },
    clearTodo(idToClear) {
      this.todos = this.todos.filter(item => item.id !== idToClear)
    },
    toggleFilter(filter) {
      this.visibility = filter
    },
    clearCompleted() {
      this.todos = this.todos.filter(item => !item.completed)
    }
  }
}
</script>

<style scoped>
  ul {
    margin: 0;
    padding: 0;
  }

  .todo {
    position: relative;
    box-shadow: 0 0 10px #555;
    padding: 0 5px;
  }

  .todo .newTodo {
    width: 100%;
    padding: 1em;
    border: none;
    outline: none;
    font: 30px Helvetica, sans-serif;
    color: #555;
  }

  .todo .toggle-all {
    position: absolute;
    left: 4px;
    top: 40px;
  }
</style>


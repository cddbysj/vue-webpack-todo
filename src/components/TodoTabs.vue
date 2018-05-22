<template>
  <div class="tabs">
    <span class="todo-count">
      <strong>{{ remaining }}</strong> {{ remaining | pluralize }} left
    </span>
    <span class="filters">
      <span        
        v-for="filter in filters"
        :key="filter"
        :class="['filter', filter === visibility?'selected':'']"
        @click="$emit('filter', filter)">
        {{ filter }}
      </span>
    </span>
    <span class="clear-completed"
      @click="$emit('clearCompleted')">
      Clear Completed
    </span>
  </div>
</template>

<script>
export default {
  props: {
    remaining: {
      type: Number,
    },
    visibility: {
      type: String,
      default: 'all'
    }
  },
  data() {
    return  {
      filters: ['all', 'active', 'completed']
    }
  },
  filters: {
    pluralize(n) {
      return n === 1? 'item' : 'items'
    }
  },
}
</script>

<style scoped>
.tabs {
  display: flex;
  justify-content: space-between;
  color: #777;
  padding: 10px 0;
}

.filter {
  cursor: pointer;
  border: 1px solid transparent;
  border-radius: 3px;
  text-align: center;
  padding: 3px 7px;
}

.filter:hover {
  border: 1px solid #bbb;
}

.selected {
  border: 1px solid #999;
}

.clear-completed:hover {
  cursor: pointer;
  text-decoration: underline;
}

</style>

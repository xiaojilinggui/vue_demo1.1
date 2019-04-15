<template>
  <footer class="footer">
      <span class="todo-count">
          <strong>{{todos.length}}</strong> 总数
      </span>
      <ul class="filters">
        <li><a href="#/all" :class="{selected: filter === 'all'}" @click="changeFilter('all')">All</a></li>
        <li><a href="#/active" :class="{selected: filter === 'active'}" @click="changeFilter('active')">Active</a></li>
        <li><a href="#/completed" :class="{selected: filter === 'completed'}" @click="changeFilter('completed')">Completed</a></li>
      </ul>
      <button class="clear-completed" @click="removeCompleted">Clear completed</button>
  </footer>
</template>

<script>

export default {
  props:{
    todos:Array,
    filter:String,
    removeCompleted:Function,
    changeFilter:Function
  },
}
</script>



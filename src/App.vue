<template>
  <div>
    <md-card-header>
      <div class="title">To-Do List</div>
    </md-card-header>
    <md-card>
      <md-field>
        <md-input v-model="currentTodo" @keydown.enter="addTodo()" placeholder=" Add a to-do here" />
      </md-field>
      <ul class="todos">
        <li v-for="todo in todos" :key="todo.id">
          <md-input type="text" v-model="todo.label" placeholder="update todo">
            <span
              v-if="todo.editing === false"
              class="editing"
              :class="{ editing: todo == editedTodo }"
              @dblclick="editTodo(todo)"
            >{{ todo.label }}</span>
          </md-input>
          <input type="checkbox" @change="completeTodo(todo)" :checked="todo.isComplete" />
          <md-button class="md-raised" @click="removeTodo(todo)">Delete To-Do</md-button>
        </li>
      </ul>
    </md-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: "",
      completed: "",
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.todos.length,
        label: this.currentTodo,
        completed: false,
        editing: false,
      });
      this.currentTodo = "";
    },
    completeTodo(todo) {
      todo.isComplete = !todo.isComplete;
    },
    editTodo(todo) {
      const index = this.todos.indexOf(todo);
      this.todos[index].editing = !this.todos[index].editing;
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
  },
};
</script>

<style>
body {
  background-color: #d3d3d3;
}
.title {
  font-size: 42px;
  text-align: center;
  margin-top: 20px;
  margin-bottom: 10px;
  color: #2a6259;
}

.md-raised {
  font-size: 20px;
  padding-top: 5px;
  padding-bottom: 5px;
  padding-left: 5px;
  color: red;
}

.md-card {
  width: 100%;
  text-align: center;
}

ul {
  list-style: none;
}

li {
  display: flex;
  padding-top: 20px;
  padding-bottom: 20px;
}
</style>

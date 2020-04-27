<template>
  <div>
    <md-card>
      <h1>Todo App</h1>
      <md-field>
        <md-input v-model="currentTodo" @keydown.enter="addTodo()" placeholder="Add new item"></md-input>
      </md-field>

      <ul class="todos">
        <li class="todo-item" v-for="todo in todos" :key="todo.id">
          <input
            class="completed"
            type="checkbox"
            @change="togglecompleted"
            v-model="todo.completed"
          />
          <span
            v-if="todo.editing === false"
            class="editing"
            :class="{ editing: todo == editedTodo }"
            @dblclick="editTodo(todo)"
          >{{ todo.label }}</span>
          <span v-if="todo.editing" class="editing">
            <md-input
              type="text"
              v-model="todo.label"
              @keyup.enter="stopEdit(todo)"
              @keyup.esc="stopEdit(todo)"
              @focusout="stopEdit(todo)"
              placeholder="Add item here"
            />
          </span>
          <button v-if="todo.editing === false" @click="editTodo(todo)">Edit</button>
          <button v-if="todo.editing === true" @click="stopEdit(todo)">Save</button>
          <button v-if="todo.editing === false" @click="removeTodo(todo)">Delete</button>
          <button v-if="todo.editing === true" @click="editTodo(todo)">Cancel</button>
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
      editedTodo: ""
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.todos.length,
        label: this.currentTodo,
        completed: false,
        editing: false
      });
      this.currentTodo = "";
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    editTodo(todo) {
      const index = this.todos.indexOf(todo);
      this.todos[index].editing = !this.todos[index].editing;
    },
    stopEdit(todo) {
      todo.editing = false;
    }
  }
};
</script>

<style>
body {
  font-family: "Roboto", sans-serif;
  font-size: 20px;
  line-height: 1.4;
  margin-left: 30px;
  margin-right: 30px;
  background-color: black;
}
.md-card {
  width: 50%;
  margin-left: auto;
  margin-right: auto;
  background-color: aquamarine;
}
ul {
  list-style-type: none;
}
div {
  padding-top: 30px;
  padding-bottom: 10px;
  padding-left: 30px;
  font-size: 20px;
}

button {
  margin: 5px;
}
span {
  padding-left: 3px;
  padding-right: 3px;
}
.editing {
  display: inline-block;
  border-radius: 5px;
}
.completed {
  width: 18px;
  height: 18px;
}
.md-field {
  border: 2px solid;
  height: 40px;
  border-radius: 10px;
  max-width: 60%;
  font-size: 20px;
  padding-top: 5px;
  padding-left: 5px;
}
.md-input {
  width: 60%;
  font-size: 20px;
}
</style>

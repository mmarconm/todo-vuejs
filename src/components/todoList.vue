<template>
  <div class="root">
    <input
      type="text"
      class="todo-input"
      placeholder="Your new Item Here..."
      v-model="newTodo"
      @keyup.enter="addTodo"
    >
    <div v-for="(todo, index) in todos" :key="todo.id">
      <div class="todo-item-left">
        <input type="checkbox" v-model="todo.completed">
        <div
          v-if="!todo.editing"
          @dblclick="editTodo(todo)"
          class="todo-item-label"
          :class="{ completed : todo.completed }"
        >{{ todo.title }}</div>
        <input
          v-else
          @blur="doneEdit(todo)"
          @keyup.enter="doneEdit(todo)"
          @keyup.esc="cancelEdit(todo)"
          class="todo-item-edit"
          type="text"
          v-model="todo.title"
          v-focus
        >
      </div>
      <div class="remove-item" @click="removeTodo(index)">&times;</div>
    </div>

    <div class="extra-container">
      <div>
        <label>
          <input type="checkbox" :checked="!anyRemaining" @change="checkAllTodos">
          Check All
        </label>
      </div>
      <div>{{ remaining }} Items Left</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "todoList",
  data() {
    return {
      beforeEditCache: "",
      todoTitle: "",
      todoId: 3,
      todos: [
        {
          id: 1,
          title: "Estudar para Prova de Sabado",
          completed: false,
          editing: false
        },
        {
          id: 2,
          title: "Fazer Trabalho com o Grupo",
          completed: false,
          editing: false
        }
      ]
    };
  },
  directives: {
    focus: {
      inserted: function(el) {
        el.focus();
      }
    }
  },
  computed: {
    remaining() {
      return this.todos.filter(todo => !todo.completed).length;
    },
    anyRemaining() {
      return this.remaining != 0;
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() == 0) {
        return;
      }
      this.todos.push({
        id: this.todoId,
        title: this.newTodo,
        completed: false
      });

      this.newTodo = "";
      this.todoId++;
    },

    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    editTodo(todo) {
      this.beforeEditCache = todo.title;
      todo.editing = true;
    },
    cancelEdit(todo) {
      todo.editing = false;
      todo.title = this.beforeEditCache;
    },
    doneEdit(todo) {
      if (todo.title.trim() == "") {
        todo.title = this.beforeEditCache;
      }
      todo.editing = false;
    },
    checkAllTodos() {
      this.todos.forEach(todo => (todo.completed = event.target.checked));
    }
  }
};
</script>

<style lang="scss">
* {
  font-family: sans-serif;
}

.todo-input {
  width: 100%;
  padding: 10px 10px;
  font-size: 18px;
  margin-bottom: 16px;

  &:focus {
    outline: 0;
  }
}

.remove-item {
  display: inline-block;
  cursor: pointer;
  margin-left: 14px;
  &:hover {
    color: black;
  }
}

.todo-item-left {
  display: flex;
  align-items: center;
}

.todo-item-label {
  padding: 10px;
  border: 1px solid white;
  margin-left: 12px;
}

.todo-item-edit {
  font-size: 24px;
  color: #2c3e50;
  margin-left: 12px;
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  font-family: "Avenir", Helvetica, Aria, sans-serif;

  &:focus {
    outline: none;
  }
}

.completed {
  text-decoration: line-through;
  color: red;
}

.extra-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: 16px;
  border-top: 1px solid lightgrey;
  padding-top: 14px;
  margin-bottom: 14px;
}

button {
  font-size: 14px;
  background-color: #fff;
  appearance: none;

  &:hover {
    outline: none;
  }
  .active {
    background-color: lightgreen;
  }
}
</style>

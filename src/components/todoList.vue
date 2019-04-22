<template>
    <div class="root">
        <input type="text" class="todo-input" placeholder="Your new Item Here..." v-model="newTodo" @keyup.enter="addTodo">
        <div v-for="(todo, index) in todos" :key=todo.id> <div>{{ todo.title }}<div class="remove-item" @click="removeTodo(index)">
            &times;
        </div></div>

        </div>
    </div>
</template>
<script>
export default {
  name: 'todoList',
  data () {
    return {
      todoTitle: '',
      todoId: 3,
      todos: [
          {
              'id': 1,
              'title': 'Estudar para Prova de Sabado',
              'completed': false,
          },
          {
              'id': 2,
              'title': 'Fazer Trabalho com o Grupo',
              'completed': false,
          },
      ]
    }
  },
  methods: {
      addTodo() {
          if(this.newTodo.trim() == 0) {
              return 

          }
            this.todos.push(
                {
                    id: this.todoId,
                    title: this.newTodo,
                    completed: false
                }
            )

          this.newTodo = '';
          this.todoId++;
      },

    removeTodo(index) {
        this.todos.splice(index,)
    }
  }
}
</script>

<style lang="scss">

* {
    font-family: sans-serif;
}

.todo-input {
    width: 100%;
    padding: 10px 10px;
    font-size: 15px;
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


</style>

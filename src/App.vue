<template>
  <div>
   
    <header>
      <h1 class="title">To Dos</h1>
    </header>

    <md-field class="addToDo"> 
      <md-input v-model="currentTodo" @keydown.enter="addTodo()" placeholder="Add a todo"></md-input>
      <md-button class="md-button md-raised" v-on:click.prevent="addTodo">
      </md-button>
    </md-field>

    <md-list class="todos" v-if="showTodos()">
      <md-list-item 
        v-for="todo in todos" 
        class="{editing: todo == editedTodo}"
        @dblclick="editedTodo(todo)"
        :key="todo.id">
        {{ todo.label }}
          <div class="view">
            <md-checkbox class="check" type="checkbox" v-model="todo.completed"></md-checkbox>
          </div>
      </md-list-item>
    </md-list>
    <md-button @click="removeTodo(todo)">Delete</md-button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: ''
    };
  },
  methods: {
    addTodo() {
      this.todos.push({id: this.todos.length, label: this.currentTodo, completed: false});
      this.currentTodo = '';
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    clickToEdit (todo) {
      this.editTodoId = todo.id; 
    },
     showTodos () {
      return this.todos.length > 0 
    },
  }
};
</script>

<style>

.todos {
  flex-flow: column;
  width: 100%;
  margin-top: 80px;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 25px 50px 0 rgba(0, 0, 0, 0.1);
}

h1 {
  width: 100%;
  text-align: center;
  color: white;
}


.addTodo{
  margin: 0 auto;
  margin-top: 20px;
  margin-bottom: 20px;
  width: 80%;
  height: 50px;
}

md-list-item {
    color: white;
}

md-button {
          outline: none;
          border: 1px solid rgb(167, 167, 167);
          padding: 1px 6px;
          color: rgb(122, 122, 122);
        }

.completed{
  text-decoration:  line-through;
}

</style>
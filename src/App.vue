<template>
  <div class="todo-app">
    <h1>To-do App</h1>
    <div v-if="!editMode">
      <div class="new-todo">
        <Button @click="newTodo">Novo</Button>
      </div>
      <todo-list 
        v-bind:todos="todos" 
        @deleteTodo="deleteTodo"
        @editTodo="editTodo"
      />
    </div>
    <todo-item 
      v-if="editMode" 
      @cancel="cancel"
      @saveTodo="saveTodo"
      :todo="todo"
    />
  </div>
</template>

<script>
  import TodoList from './components/TodoList.vue';
  import TodoItem from './components/TodoItem.vue';

export default {
  components: {
    TodoList,
    TodoItem
  },
  data() {
    return {
      editMode: false,
      todos: [],
      todo: null,
      nextId: 1
    }
  },
  methods: {
    newTodo() {
      this.editMode = true;
      this.todo = null;
    },
    cancel() {
      this.editMode = false;
    },
    saveTodo(todo) {
      if(todo.id) {
        // Edição

        const index = this.todos.findIndex((item) => item.id === todo.id);
        this.todos[index] = todo;
      } else {
        // Inclusão
        
        todo = { id: this.nextId, ...todo }
        this.todos.push(todo);
        localStorage.setItem("todos", JSON.stringify(this.todos));
        this.nextId++;
      }
      localStorage.setItem("nextId", this.nextId);
      this.editMode = false;

    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
    editTodo(index) {
      this.todo = this.todos[index];
      this.editMode = true;
    }
  },
  created() {
    const todos = localStorage.getItem("todos");
    if(todos) {
      this.todos = JSON.parse(todos);
    }

    const nextId = localStorage.getItem("nextId");
    if(nextId) {
      this.nextId = parseInt(nextId);
    }
  }
}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
  }

  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    min-height: 100vh;
    color: #fff;
    background-color: #482880;
    padding: 1px;
  }

  .todo-app {
    margin-top: 2rem;
  }

  .todo-app h1 {
    text-align: center;
    text-decoration:  4px underline #673ab7;
  }

  .new-todo {
    display: flex;
    justify-content: flex-end;
    margin: 1rem;
    padding: 0 1rem;
  }

</style>

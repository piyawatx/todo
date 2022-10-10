<template>
  <div class="todo">
    <div class="container-fluid bg-dark">
      <div class="container p-0 vh-100">
        <div class="card card-body bg-dark ">
          <h1 class="text-white">Todo App</h1>

          <div class="d-flex">
            <input
              type="text"
              class="form-control"
              placeholder="Add your new todo"
              v-model="newTodo"
            />
            <button
              type="button"
              class="btn btn-primary ms-2"
              @click="addTodo()"
            >
              Add
            </button>
          </div>

          <div
            class="d-flex justify-content-between rounded bg-white mt-1 p-1 px-3"
            v-for="(todo, n) in todos"
            :key="n"
          >
            <div class="align-middle">
              {{ todo }}
            </div>
            <button type="button" class="btn btn-danger" @click="removeTodo(n)">
              Remove
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      newTodo: null,
    };
  },
  mounted() {
    if (localStorage.getItem("todos")) {
      try {
        this.todos = JSON.parse(localStorage.getItem("todos"));
      } catch (e) {
        localStorage.removeItem("todos");
      }
    }
  },
  methods: {
    addTodo() {
      if (!this.newTodo) {
        return;
      }
      this.todos.push(this.newTodo);
      this.newTodo = "";
      this.saveTodos();
    },
    removeTodo(x) {
      this.todos.splice(x, 1);
      this.saveTodos();
    },
    saveTodos() {
      const parsed = JSON.stringify(this.todos);
      localStorage.setItem("todos", parsed);

      console.log(localStorage.todos);
    },
  },
};
</script>

<style scoped>
</style>
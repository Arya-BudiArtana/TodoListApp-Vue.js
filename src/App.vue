<template>
  <div class="container mt-1">
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">MY TODO APP</h5>
        <div class="row">
          <div class="col-10">
            <input
              type="text"
              v-model="todo"
              class="form-control"
              @keyup.enter="add"
            />
          </div>
          <div class="col-2">
            <button class="btn btn-success" @click="add">ADD</button>
          </div>
        </div>
        <list :todos="todos" @deleteList="deleteList" @done="done" />
        <small>{{ totalTodo }}</small>
      </div>
    </div>
  </div>
</template>

<script>
import List from "./assets/components/List.vue";
export default {
  components: {
    List,
  },
  data() {
    return {
      todo: "",
      todos: [],
    };
  },

mounted() {
    this.todos = JSON.parse(localStorage.getItem('todos'))
},
  computed: {
    totalTodo() {
      return this.todos.length;
    },
  },

  methods: {
    add() {
      this.todos.unshift({
        activity: this.todo,
        isDone: false,
      });
      this.todo = "";
      this.saveTodo();
    },

    deleteList(todoIndex) {
      this.todos = this.todos.filter((item, index) => {
        if (index != todoIndex) {
          return item;
        }
      });
      this.saveTodo();
    },

    done(todoIndex) {
      this.todos = this.todos.filter((item, index) => {
        if (index == todoIndex) {
          item.isDone = false;
        }

        if (index == todoIndex) {
          item.isDone = true;
        }


        return item;
      });

      this.saveTodo();
    },
    saveTodo() {
        localStorage.setItem('todos', JSON.stringify(this.todos))
    }
  },
};
</script>

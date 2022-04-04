<template>
  <div class="ms-3 mt-3">
    <ul class="list-group">
      <li v-for="(todo, index) in todos" :key="index" class="list-group-item">
        <div class="row">
            <div class="col">
                <span v-if = "todo.isDone">
                    <del>{{todo.activity}}</del>
                </span>
                <span v-else>{{todo.activity}}</span>
            </div>
            <div class="col-auto">
                <div class="row gx-2">
                    <div class="col">
                        <button @click="deleteTODO(index)" class="btn-danger btn m-2">X</button>
                        <button class="btn btn-info" @click="doneTODO(index)">{{todo.isDone ? "Undone" : "Done"}}</button>
                    </div>
                </div>
            </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    todos: {
      type: Array,
      default: [],
    },
  },

  methods: {
      deleteTODO(index) {
          this.$emit("deleteList", index);
      },

      doneTODO(index) {
          this.$emit("done", index);
      }
  }
};
</script>

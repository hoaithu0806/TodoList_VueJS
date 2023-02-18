<template>
  <div class="container">
    <h2 class="text-center mt-5">My VueJS TodoList</h2>

    <!-- Input -->
    <div class="d-flex">
      <input
        v-model="task"
        type="text"
        placeholder="Enter task"
        class="form-control"
      />
      <button v-on:click="submitTask" class="btn btn-warning rounded-0">
        ADD
      </button>
    </div>
    <!-- Task table -->
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col">Status</th>
          <th scope="col" class="text-center">Option</th>
          <th scope="col" class="text-center">Option</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" v-bind:key="index">
          <td>{{ task.name }}</td>
          <td>
            <span v-on:click="changeStatus(index)" class="pointer">{{
              task.status
            }}</span>
          </td>
          <td>
            <div class="text-center" v-on:click="editTask(index)">
              <button class="btn btn-info rounded-0">Edit</button>
            </div>
          </td>
          <td>
            <div class="text-center" v-on:click="deleteTask(index)">
              <button class="btn btn-danger rounded-0">Delete</button>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: {
    msg: String
  },
  data() {
    return {
      task: "",
      editedTask: null,
      availableStatuses: ["To-do", "In-progress", "Finished"],
      tasks: [
        {
          name: "Cài đặt môi trường VueJS",
          status: "To-do"
        },
        {
          name: "Bài tập thực hành Todo list",
          status: "In-progress"
        },
        {
          name: "Cách xử lý sự kiện trong VueJS",
          status: "Finished"
        }
      ]
    };
  },
  methods: {
    submitTask() {
      if (this.task.length === 0) return;
      if (this.editedTask === null) {
        this.tasks.push({
          name: this.task,
          status: "to-do"
        });
      } else {
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      }
      this.task = "";
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    editTask(index) {
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },
    changeStatus(index) {
      let newIndex = this.availableStatuses.indexOf(this.tasks[index].status);
      if (++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.availableStatuses[newIndex];
    }
  }
};
</script>

<style>
.pointer {
  cursor: pointer;
}
</style>

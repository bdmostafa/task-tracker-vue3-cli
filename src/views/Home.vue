<template>
  <AddTask v-show="isAddTaskForm" @add-task="addTask" />
  <Tasks
    @toggle-reminder="toggleReminder"
    @remove-task="removeTask"
    :tasks="tasks"
  />
</template>

<script>
import Tasks from "../components/Tasks.vue";
import AddTask from "../components/AddTask.vue";

export default {
  name: "Home",
  props: {
    isAddTaskForm: {
      type: Boolean,
      default: false,
    },
  },
  inheritAttrs: false, // disable 'non-props' warning
  components: {
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    async removeTask(id) {
      if (confirm("Are you sure to delete this task?")) {
        const res = await fetch(`api/tasks/${id}`, {
          method: "DELETE",
        });

        res.status === 200
          ? (this.tasks = this.tasks.filter((task) => task.id !== id))
          : alert("Oops... Error in removing task");
      }
    },
    async toggleReminder(id) {
      const taskToToggle = await this.fetchTask(id);

      const updateTask = { ...taskToToggle, reminder: !taskToToggle.reminder };

      const res = await fetch(`api/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(updateTask),
      });

      const data = await res.json();
      this.tasks = this.tasks.map((task) => {
        // return task.id === id ? { ...task, reminder: !task.reminder } : task;
        return task.id === id ? { ...task, reminder: data.reminder } : task;
      });
    },
    async addTask(task) {
      const res = await fetch("api/tasks", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(task),
      });

      const data = await res.json();

      // this.tasks = [...this.tasks, task];
      this.tasks = [...this.tasks, data];
    },
    async fetchTasks() {
      const res = await fetch("api/tasks");

      const data = await res.json();

      return data;
    },
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`);

      const data = await res.json();

      return data;
    },
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
};
</script>

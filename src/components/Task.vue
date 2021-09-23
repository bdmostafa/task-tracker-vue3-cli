<template>
  <div
    @dblclick="toggleReminder(task.id)"
    :class="[task.reminder ? 'reminder' : '', 'task']"
  >
    <h4>
      {{ task.title }}
      <i @click="removeTask(task.id)" class="fas fa-trash"> </i>
    </h4>
    <p>{{ task.day }}</p>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: {
    task: Object,
  },
  methods: {
    removeTask(id) {
      this.$emit("remove-task", id);
    },
    toggleReminder(id) {
      this.$emit("toggle-reminder", id);
    },
  },
};
</script>

<style scope>
.fas {
  color: red;
}
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.task.reminder {
  border-left: 5px solid green;
}
.task h4 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>

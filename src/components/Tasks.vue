<template>
    <div v-for="task in tasks" :key="task.id">
        <Task @remove-task="$emit('remove-task', task.id)" :task="task" />
    </div>
</template>

<script>
import Task from "./Task.vue"

export default {
    name: "Tasks",
    components: {
        Task
    },
    props: {
        tasks: Array
    },
    emits: ['remove-task']
}
</script>

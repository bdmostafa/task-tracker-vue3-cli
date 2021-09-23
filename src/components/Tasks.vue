<template>
    <div v-for="task in tasks" :key="task.id">
        <h4> {{ task.title }} </h4>
    </div>
</template>

<script>

export default {
    name: "Tasks",
    props: {
        tasks: Array
    }
}
</script>

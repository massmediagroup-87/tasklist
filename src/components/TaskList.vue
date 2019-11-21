<template>
    <ol class="list-group">
        <task
                :checkAll="checkAll"
                :key="task.id"
                :todo="task"
                v-for="task in tasks"
        />
    </ol>
</template>

<script>
    import Task from "./Task";

    export default {
        name: "TaskList",
        components: {
            Task
        },
        props: {
            'tasks': Array,
            'checkAll': Boolean
        }
    }
</script>
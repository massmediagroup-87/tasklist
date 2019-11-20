<template>
    <ol class="list-group">
        <task
                :key="task.id"
                :status="status"
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
            status: {
                type: Boolean
            }
        },
        data: () => ({
            tasks: []
        }),
        created() {
            let tasks = JSON.parse(localStorage.getItem('tasks'));

            if(tasks !== null) {
                tasks.forEach((task) => {
                    this.tasks.push(task)
                })
            }

            this.$parent.$on('add-task', this.addTask);
        },
        methods: {
            addTask(text) {
                if(text.length > 2) {
                    this.tasks.unshift({text})
                }
                localStorage.tasks = JSON.stringify(this.tasks);
            }
        }

    }
</script>

<style scoped>

</style>
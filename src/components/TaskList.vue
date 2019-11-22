<template>
    <ol class="list-group">
        <task
                :checkAll="checkAll"
                :key="task.id"
                :todo="task"
                @destroy="destroyTask"
                @checked-task="checkedTask"
                v-for="task in sortedTasks"
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
            tasks: Array,
            checkAll: Boolean
        },
        methods: {
            compare(a) {
                if (a.active) {
                    return -1;
                } else {
                    return 1;
                }
            },
            checkedTask(id) {
                this.$emit('checked-task', id)
            },
            destroyTask(id) {
                this.$emit('remove', id)
            }
        },
        computed: {
            sortedTasks() {
                return [...this.tasks].sort(this.compare);
            }
        }
    }
</script>
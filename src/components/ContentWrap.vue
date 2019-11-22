<template>
    <div>
        <input-title @add-task="addTask"/>
        <div class="custom-control custom-checkbox mr-sm-2 mb-3">

            <input
                    class="custom-control-input"
                    id="customControlAutosizing"
                    type="checkbox"
                    v-model="checked">

            <label class="custom-control-label" for="customControlAutosizing">Show all tasks</label>

        </div>

        <task-list
                :check-all="checked"
                :tasks="tasks"
                @remove="destroyTask"
                @checked-task="checkedTask"/>

    </div>
</template>

<script>
    import TaskList from "./TaskList";
    import InputTitle from "./InputTitle";

    export default {
        name: "ContentWrap",
        components: {
            InputTitle,
            TaskList
        },
        data: () => ({
            checked: false,
            tasks: []
        }),
        updated() {
            this.setStorage('checked', this.checked);
        },
        created() {
            this.addTaskStorage();
            this.$on('checked-task', this.checkedTask);
            if (this.getStorage('checked')) this.checked = this.getStorage('checked');
        },
        methods: {
            getStorage(key) {
                return JSON.parse(localStorage.getItem(key));
            },
            setStorage(key, value) {
                localStorage[key] = JSON.stringify(value);
            },
            addTask(text) {
                if (text.length > 2) {
                    this.tasks.unshift({
                        id: new Date().getTime(),
                        text: text,
                        active: false
                    })
                }

                this.setStorage('tasks', this.tasks);
            },
            addTaskStorage() {
                let tasks = this.getStorage('tasks');

                if (tasks !== null) {
                    tasks.forEach((task) => {
                        this.tasks.push(task)
                    })
                }
            },
            checkedTask(id) {
                this.tasks.forEach((item, index) => {
                    if (this.tasks[index].id === id) {
                        this.tasks[index].active = !this.tasks[index].active;
                    }
                });

                this.setStorage('tasks', this.tasks);
            },
            destroyTask(id) {
                this.tasks = this.tasks.filter(item => item.id !== id);
                this.setStorage('tasks', this.tasks);
            }
        }
    }
</script>

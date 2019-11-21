<template>
    <div>
        <input-title/>
        <div class="custom-control custom-checkbox mr-sm-2 mb-3">
            <input class="custom-control-input" id="customControlAutosizing" type="checkbox" v-model="checked">
            <label class="custom-control-label" for="customControlAutosizing">Show all tasks</label>
        </div>
        <task-list :check-all="checked" :tasks="tasks"/>
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
            tasks: [],
            text: ''
        }),
        updated() {
            this.setStorage('checked', this.checked);

            this.sortTasks(this.tasks);
        },
        created() {
            this.addTaskStorage();

            if (this.getStorage('checked')) this.checked = this.getStorage('checked');

            this.$on('add-task', this.addTask);
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
            sortTasks(arr) {
                for (let i = 0, endI = arr.length - 1; i < endI; i++) {
                    let wasSwap = false;

                    for (let j = 0, endJ = endI - i; j < endJ; j++) {
                        if (arr[j].active < arr[j + 1].active) {
                            [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
                            wasSwap = true;
                        }
                    }

                    if (!wasSwap) break;
                }
                return arr;
            }
        }
    }
</script>

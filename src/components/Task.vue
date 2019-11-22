<template>
    <li
        class="list-group-item alert alert-warning alert-dismissible fade show mb-2"
        role="alert"
        v-if="checkAll ? true : !checked">

        {{ todo.text }}

        <label aria-label="Close" class="close mr-4" data-dismiss="alert">

            <input
                    aria-label="Checkbox for following text input"
                    type="checkbox"
                    v-model="checked"
                    @change="checkedTask">

            <span aria-hidden="true" class="mr-4"></span>

        </label>

        <button
                @click="destroyTask"
                aria-label="Close"
                class="close"
                data-dismiss="alert"
                type="button"
                v-if="checked">

            <span aria-hidden="true">&times;</span>
        </button>
    </li>
</template>

<script>

    export default {
        name: "Task",
        props: {
            todo: Object,
            checkAll: Boolean
        },
        data: () => ({
            checked: false
        }),
        created() {
            if (this.todo.active) this.checked = true;
        },
        methods: {
            checkedTask() {
                this.$emit('checked-task', this.todo.id);
            },
            destroyTask() {
                this.$emit('destroy', this.todo.id);
            }
        }
    }
</script>
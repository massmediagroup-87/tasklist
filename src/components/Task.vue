<template>
    <li v-if="!status ? !checked : true" class="list-group-item alert alert-warning alert-dismissible fade show mb-2" role="alert">
        {{ todo.text }}
        <label class="close" data-dismiss="alert" aria-label="Close">
            <input v-model="checked" type="checkbox" aria-label="Checkbox for following text input">
        </label>
    </li>
</template>

<script>
    export default {
        name: "Task",
        props: {
            'todo': {
                type: Object
            },
            'status' : {
                type: Boolean
            }
        },
        data: function () {
            return {
                checked: false
            }
        }
    }
</script>

<style scoped>

</style>
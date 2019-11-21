<template>
    <div class="input-group mb-3">
        <input aria-describedby="basic-addon2" class="form-control" placeholder="Add task" type="text" v-model="text">
        <button @click="addTask" class="btn btn-primary">Add</button>
    </div>
</template>

<script>

    export default {
        name: "InputTitle",
        components: {},
        data: () => ({
            text: ''
        }),
        methods: {
            addTask() {
                this.$parent.$emit('add-task', this.text);

                this.text = '';
            }
        },
        updated() {
            this.$parent.text = this.text;
        }
    }

</script>
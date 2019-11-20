<template>
    <div>
        <input-title/>
        <div class="custom-control custom-checkbox mr-sm-2 mb-3">
            <input v-model="checked" type="checkbox" class="custom-control-input" id="customControlAutosizing">
            <label class="custom-control-label" for="customControlAutosizing">Show all tasks</label>
        </div>
        <task-list :status="checked"/>
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
        data: ()=> ({
            checked: false
        })
    }
</script>

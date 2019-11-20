<template>
    <div class="container" id="app">

        <h1 class="text-center mt-4">My task list</h1>

        <content-wrap></content-wrap>

    </div>
</template>

<script>
    import ContentWrap from "./components/ContentWrap";

    export default {
        name: "app",
        components: {
            ContentWrap
        }
    }
</script>


<script setup>
import Panes from "./components/Panes.vue";
import Pane from "./components/Pane.vue";</script>

<template>
    <panes style="height: 500px">
        <pane default-size="300px" style="min-height: 200px">
            Pane #1
        </pane>
        <pane>
            Pane #2
        </pane>
        <pane>
            Pane #3
        </pane>
    </panes>
</template>

<style lang="less">

</style>

<template>
    <div class="panes" :class="{horizontal}" :id="`panes-${id}`">
        <slot/>
    </div>
</template>

<script setup>
import { provide } from "vue";

const props = defineProps({
    horizontal: { type: Boolean, default: false },
})

const id = Math.random().toString(16).substring(2)

provide('horizontal', props.horizontal)
provide('panesId', id)
</script>

<style lang="less">
.panes {
    display: flex;
    box-sizing: border-box;
    border: solid 3px #000;
    flex-direction: column;
    margin: 0;
    padding: 0;

    &.horizontal {
        flex-direction: row;
    }
}
</style>
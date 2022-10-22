<template>
    <div
        ref="splitter"
        class="splitter"
        :class="{active}"
        @mousedown="onMouseDown"
        @mouseup="onMouseUp"
    />
</template>
<script setup>
import { computed, inject, ref } from "vue";

const active = ref(false)
const splitter = ref(null)
const emit = defineEmits([ 'active', 'inactive' ])
const horizontal = inject('horizontal')
const axis = computed(() => horizontal ? 'X' : 'Y')

const onMouseDown = event => {
    active.value = true
    window.addEventListener('mouseup', onMouseUp, { once: true })
    emit('active', event[`client${axis.value}`])
}

const onMouseUp = () => {
    active.value = false
    emit('inactive')
}
</script>

<style lang="less">
.panes {
    .splitter {
        user-select: none;
        display: flex;
        justify-content: center;

        &:last-child {
            display: none;
        }

        &:before {
            display: block;
            content: '';
            padding: 0.2em;
            background-color: antiquewhite;
        }

        &.active:before, &.active:hover:before {
            background-color: red;
        }

        &:hover:before {
            background-color: cornflowerblue;
        }
    }

    &.horizontal {
        .splitter {
            width: 2em;
            cursor: ew-resize;
            flex-direction: row;

            &:before {
                margin: 0 0.8em;
            }

        }
    }

    &:not(.horizontal) {
        .splitter {
            height: 2em;
            cursor: ns-resize;
            flex-direction: column;

            &:before {
                margin: 0.8em 0;
            }
        }
    }
}
</style>
<template>
    <div class="pane" ref="pane" v-bind="$attrs">
        <slot/>
    </div>
    <splitter ref="splitter" @active="start" @inactive="stop"/>
</template>

<script setup>
import Splitter from './Splitter.vue'
import { computed, inject, onMounted, ref } from "vue";

const props = defineProps({
    defaultSize: { type: String, default: 'auto' },
})
const pane = ref(null)

const horizontal = inject('horizontal')

const dimension = computed(() => horizontal ? 'width' : 'height')
const axis = computed(() => horizontal ? 'X' : 'Y')
const dimensionProps = computed(() => horizontal ? 'clientWidth' : 'clientHeight')

onMounted(() => pane.value.style[dimension.value] = props.defaultSize)

let resize = null
const panesId = `panes-${inject('panesId')}`
const onMouseMove = e => resize?.(e[`client${axis.value}`])

const start = length0 => {
    const origin = pane.value[dimensionProps.value]
    const offset = origin - length0
    resize = length1 => {
        const target = length1 + offset
        pane.value.style[dimension.value] = `${target}px`
    };
    window.addEventListener('mousemove', onMouseMove, { capture: true })
}

const stop = () => {
    window.removeEventListener('mousemove', onMouseMove)
    resize = null;
}
</script>

<style lang="less">
.panes .pane {
    margin: 0;
    padding: 0;
    min-height: fit-content;
    min-width: fit-content;
}
</style>
<template>
    <div>
        Mouse position is at: {{ x }}, {{ y }}
    </div>
    <div>
        {{city}} - {{time}}
    </div>
    <p>valor1: {{valor1}}</p>
</template>

<script setup>
import { onMounted, onUnmounted, onUpdated, reactive, ref, watch, inject } from 'vue';
import { useMouse } from '../composable/mouse';


const { x, y } = useMouse()
const time = ref(0)

setInterval(() => {
    time.value++
}, 1000)
const city = reactive({
    name: 'Ambato',
    country: 'Ecuador'
})

watch(time,(newValue,oldValue) => {
    console.log(newValue,oldValue)

})

const valor1 = inject('valor1')  //inject

console.log("setup")

onMounted(() => {
    console.log('mounted')
})
onUpdated(() => {
    console.log('updated')
})
onUnmounted(() => {
    console.log('unmounted')
})

</script>

<style lang="scss" scoped>

</style>
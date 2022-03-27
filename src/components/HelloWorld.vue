<template>
  <h3>{{ msg }} - {{mayus}}</h3>
  <h3>{{ msg2 }} - {{mayus2}}</h3>
  <h4>{{count}}</h4>
  <button @click="count++">+1</button>
  <button @click="$emit('change')">enviar cambio</button>
  <button @click="$emit('change2', 'hola', count)">enviar datos</button>
  <br> <br>
</template>

<script setup> 
import { computed } from '@vue/reactivity';
import { ref,toRefs } from 'vue'

const count = ref(0)

const props = defineProps({
  msg: String,
  msg2: String
})

// const mayus = computed(()=> props.msg.toUpperCase())
// const mayus2 = computed(()=> props.msg2.toUpperCase())

const {msg, msg2} = toRefs(props) 
const mayus = computed(()=> msg.value.toUpperCase())
const mayus2 = computed(()=> msg2.value.toUpperCase())

const emit = defineEmits([
  'change',
  'change2'
])


//defineExpose({mayus2}) //Para exponer explícitamente las propiedades de un componente
</script>

<style scoped>
a {
  color: #42b983;
}
</style>

<template>
  <div id="inicio">
    <img alt="Vue logo" src="./assets/logo.png" width="100" />
  </div>
  <Mouse />

  <div>
    <input type="text" v-model="msg2" ref="input">
  </div>

  <HelloWorld msg="Hello Vue 3 + Vite" :msg2=msg2 @change="change" @change2="change2" />

  <button @click="show = !show">toggle</button>

  <Transition>
    <div v-show="show">
      <h1>hola</h1>
    </div>
  </Transition>

  <Transition name="bounce">
    <p v-if="show" style="text-align: center;">Hello here is some bouncy text!</p>
  </Transition>

  <teleport to="#inicio">
    <p v-if="show">GIANC</p>
  </teleport>


</template>

<script setup>import { defineAsyncComponent, ref, onMounted } from 'vue';
//setup se ejecuta antes del ciclo de vida
import Mouse from './components/Mouse.vue';
import { provide } from 'vue'

//defineAsyncComponent: Define an async component which is lazy loaded only when it is rendered.
const HelloWorld = defineAsyncComponent(() => import("./components/HelloWorld.vue"))

const show = ref(false)
const msg2 = ref("msg2")

const change = () => {
  console.log("change")
}
const change2 = (a,b) => {
  console.log("change2:",a,b)
}


provide('valor1', 10)  //provide

const input = ref(null)
//console.log(input) //daria null porque setup se ejeuta antes que el ciclo de vida
onMounted(() => {
  input.value.select()
  console.log("input.value:",input.value)
})
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 10px;
}
.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
.bounce-enter-active {
  animation: bounce-in 0.5s;
}
.bounce-leave-active {
  animation: bounce-in 0.5s reverse;
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.25);
  }
  100% {
    transform: scale(1);
  }
}
</style>

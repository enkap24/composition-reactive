<script setup>
import { ref } from "vue";

let msg = "Hello friends";
let refMsg = ref(msg);

function logChange() {
  console.log(`msg value: ${msg}`);
  console.log(`refMsg value: ${refMsg.value}`);
}
// component logic
// declare some reactive state here.
</script>

<template>
  <h1>{{ msg }}</h1>
  <h1>{{ refMsg }}</h1>
  <input v-model="msg" /> <br />
  <input v-model="refMsg" />
  <!-- first comment this `input v-model="refMsg"` line out and see -->
  <br />
  <button @click="logChange">log change</button>
</template>
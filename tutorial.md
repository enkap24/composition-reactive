Intro
* The examples here are about the composition API
* Making data reactive in the composition API is not as straightforward as with the options API
* `reactive` means when changed, it is reflected on the UI in other places
* To make data reative, you have to import `ref` or `reactive` from `vue`
* You can quickly test the examples below by 
    * Go to [code sandbox](https://codesandbox.io/)
    * Create a vue sandbox
    * paste the code in the `app.vue` file

## ref
* It is used to make primitive values reactive
* See the example below along with the comments


```
<script setup>
  import { ref} from 'vue'

  let msg = "Hello friends";
  let refMsg = ref(msg);
  
  function logChange(){
    console.log(`msg value: ${refMsg.value}`); //notice that you access it be using `.value` <!-- 1 -->
    console.log(`msg value: ${msg}`);
  }
</script>

<template>
 
  
  msg input: <input v-model="msg"> <br/>
  <h1>{{msg}}</h1>
  refMsg input: <input v-model="refMsg"> <br/> <!-- 1 -->
  <h1>{{refMsg}}</h1> <!-- notice that in html it is referenced directly without the '.value' suffix --> <!-- 1 -->
  <button @click="logChange">
    log change
  </button>
</template>
```
### Excercise
* change the input data of `refMsg input:` first and see the changes then notice changes displayed in text below.
* Now change the input data of `msg input:`. No change is visible until you start changing the data of `refMsg input:`


## reactive 
* reactive is used to make non-primitive objects reactive

```
<script setup>
import { reactive } from 'vue'

  let car = {mark: "audi", colour: "silver"};
  let reCar = reactive(car);
  
  function logChange(){
    console.log(`refMsg value: ${car.colour}`);
    console.log(`refMsg value: ${reCar.colour}`);
  }
</script>

<template>
  car: <input v-model="car.colour"><br/>
  <h1>{{car.colour}}</h1>
  reactive car: <input v-model="reCar.colour"><br/>
  <h1>{{reCar.colour}}</h1>
  <button @click="logChange">
    log change
  </button>
</template>
```
### Excercise
* Change the data in the `car:` input and notice that you do not see changes
* Change the data in `reactive car:` input and notice that changes are visible in both inputs and outputs

* see reactive and ref limitations [here](https://vuejs.org/guide/essentials/reactivity-fundamentals.html#limitations-of-reactive)

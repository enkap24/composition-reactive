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
    console.log(`car.colour value: ${car.colour}`);
    console.log(`reactCar.colour value: ${reCar.colour}`); <!-- 1 -->
  }
</script>

<template>
  car: <input v-model="car.colour"><br/>
  <h1>{{car.colour}}</h1>
  reactive car: <input v-model="reCar.colour"><br/>
  <h1>{{reCar.colour}}</h1>.   <!-- 1 -->
  <button @click="logChange">
    log change
  </button>
</template>
```
### Excercise
* Change the data in the `car:` input and notice that you do not see changes
* Change the data in `reactive car:` input and notice that changes are visible in both inputs and outputs
* Notice in `<!-- 1 -->` above that with reactive the `.value` suffix is never used

* see reactive and ref limitations [here](https://vuejs.org/guide/essentials/reactivity-fundamentals.html#limitations-of-reactive)


## Reactive vs ref
* Below is an example of `ref` and `reactive` on arrays
* In the exercises you will see that `reactive` is not that reactive when removing values from arrays


```
<script setup>
import { ref, reactive } from 'vue'

let id = 0

const newTodo = ref('');
const hideCompleted = ref(false);
let todos = reactive([
  { id: id++, text: 'Learn HTML', done: true },
  { id: id++, text: 'Learn JavaScript', done: true },
  { id: id++, text: 'Learn Vue', done: false }
]);
let refTodos = ref([
  { id: id++, text: 'Learn HTML', done: true },
  { id: id++, text: 'Learn JavaScript', done: true },
  { id: id++, text: 'Learn Vue', done: false }
]);


function addTodo() {
  todos.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos = todos.filter((t) => t !== todo)
}
function addRefTodo() {
  refTodos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}

function removeRefTodo(todo) {
  refTodos.value = refTodos.value.filter((t) => t !== todo)
}
</script>

<template>
    <form @submit.prevent="addTodo">
    <input v-model="newTodo">
    <button>Add Todo</button>
  </form>

  <ul>
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.text }}
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  
  
  <h1>
    RefTodos
  </h1>
    <form @submit.prevent="addRefTodo">
    <input v-model="newTodo">
    <button>Add Todo</button>
  </form>
    <ul>
    <li v-for="todo in refTodos" :key="todo.id">
      {{ todo.text }}
      <button @click="removeRefTodo(todo)">X</button>
    </li>
  </ul>

</template>

<style>
.done {
  text-decoration: line-through;
}
</style>
```





<template>
  <div class="container text-center mt-3">
  <h1>Hola {{ name.toUpperCase() }}</h1>
  <h2 :class="classCounter">
    {{ counter}}
  </h2>
  <div class="btn-group">
  <button @click="increment" class="btn btn-success">Aumentar</button>
  <button @click="decrement" class="btn btn-danger">Disminur</button>
  <button @click="reset" class="btn btn-secondary">Reset</button>
  <button @click="add" :disabled="blockNumber" class="btn btn-primary">Add</button>
</div>
  <ul class="list-group mt-4">
    <li
    class="list-group-item"
    v-for="(item, index) in arrayCounter" :key="index">
      {{ item }}
    </li>
  </ul>
</div>
</template>

<script setup>
import {ref, computed} from 'vue';

    const name = "vue dinamico";
   
const counter = ref (0);
const arrayCounter = ref([]);


const increment = () => {
 counter.value ++;
};
const decrement = () => {
  counter.value --;
};
//anfn se coloca automaticamente la funcion de flecha
const reset = () => {
  (counter.value = 0);
};

const add = () => {
  arrayCounter.value.push(counter.value);
};

const blockNumber = computed(() => {
  const number = arrayCounter.value.find((num) => num === counter.value);
  return number || number === 0;
});



const classCounter = computed (() => {
  if(counter.value === 0) {
    return 'zero'
  }
  return counter.value > 0 ? "positive" : "negative";
});

</script>



<style scoped>
h1 {
  color: red;
}
.positive{
  color:rgb(18, 135, 18);
}
.negative{
  color: red;
}
.zero {
  color: maroon
}
</style>
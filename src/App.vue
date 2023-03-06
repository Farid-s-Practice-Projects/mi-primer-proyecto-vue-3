<script setup>
import {ref,computed} from "vue"

const user="Farid";
//REACTIVIDAD -> VARIABLE REACTIVA CON REF (PARA QUE CAMBIEN DINAMICAMENTE EN EL HTML)
let counter=ref(0);
const arrayNumbers=ref([]);
const increment=()=>{
  counter.value++;
  console.log(counter.value);
}
const decrease=()=>{
  counter.value--;
  console.log(counter.value);
}
const reset=()=>{
  counter.value=0;
  console.log(counter.value);
}

const addNumber = () =>{
  arrayNumbers.value.push(counter.value);
}

const blockBtnAdd = computed(() => {
 const numSearch = arrayNumbers.value.find(num=>num===counter.value);
 console.log(numSearch);
 if(numSearch===0){ return true; }
 return numSearch ? true : false;
  /*return numSearch || numSearch === 0;*/
})

//se recomienda utilizar computed en vez de un metodo, cuando se trabajan con datos reactivos
const classCounter= computed(() =>{
  if(counter.value===0){
    return 'zero'
  }
  if(counter.value<0){
    return 'negative'
  }
  if(counter.value>0){
    return 'positive'
  }
})

</script>

<template>

  <div class="container text-center mt-5">
    <h1 class="title mb-4">Welcome to practice Vue js 3, {{user}}</h1>
    <div class="btn-group mb-4">
      <button @click="decrease" class="btn btn-danger">Disminuir</button>
      <button @click="reset" class="btn btn-primary">Resetear</button>
      <button @click="increment" class="btn btn-success">Aumentar</button>
      <button @click="addNumber" class="btn btn-secondary" :disabled="blockBtnAdd">Add</button>
    </div>

    <h2 :class="classCounter">{{counter}}</h2>

    <h2 class="subtitle mt-4">Lista de mis números favoritos:</h2>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="(num,index) in arrayNumbers" :key="index">
        {{num}}
      </li>
    </ul>
  </div>


</template>

<style>
.positive{
  color:green;
}
.negative{
  color:red;
}
.zero{
  color:peru;
}
.title{
  color:green;
}
.subtitle{
  color: green ;
}
</style>
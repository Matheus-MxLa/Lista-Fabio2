<script setup>
import { ref } from 'vue';
const tarefas = ref(['Tarefa 1', 'tarefa 2', 'tarefa 3']);
const novaTarefa = ref('');
const posAlternada = ref(-1);

function addTarefa() {
  if (posAlternada.value == -1) {
    if(novaTarefa.value.trim().length >= 5) {
      tarefas.value.push(novaTarefa.value);
    }
  }
  else {
    tarefas.value.splice(posAlternada.value, 1, novaTarefa.value);
    posAlternada.value = -1;
  }
  novaTarefa.value = '';
}
function delTarefa(item) {
  const posicao = tarefas.value.indexOf(item);
  tarefas.value.splice(posicao, 1);
}
function ordenarTarefa() {
  tarefas.value.sort();
}
function ediTarefa(item) {
  posAlternada.value = tarefas.value.indexOf(item);
  novaTarefa.value = item;
}
</script>

<template>
<div class="container">
  <h1>Lista de Tarefas</h1>
  <input type="text" v-model="novaTarefa">
  <button @click="addTarefa">Add</button>
  <ul>
    <li v-for="tarefa in tarefas" :key="tarefa">
      {{ tarefa }}
      <span>
        <a href="#" @click.prevent="ediTarefa(tarefa)" >Editar</a>
        <a href="#" @click.prevent="delTarefa(tarefa)" >Delete</a>
      </span>
    </li>
  </ul>
  <button @click="ordenarTarefa">Ordenar</button>
</div>
</template>

<style scoped>
span a {
  color: rgb(255, 0, 0);
}
</style>

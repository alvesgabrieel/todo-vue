<script setup>

import { toValidAssetId } from '@vue/compiler-core';
import { reactive } from 'vue';


const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [
    {
      titulo: 'Estudar TypeScript',
      finalizada: false
    },
    {
      titulo: 'Estudar Node.js',
      finalizada: false
    },
    {
      titulo: 'Estudar Ingles',
      finalizada: true
    },
  ]
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada); //itera sobre cada item do array, e retorna o valor pedido (tarefas finalizadas);
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada);
}

const filtarTarefas = () => {
  const { filtro  } = estado;

  switch(filtro) {
    case 'pendentes':
      return getTarefasPendentes();
    case 'finalizadas':
      return getTarefasFinalizadas()
    default:
      return estado.tarefas;
  }
}

const cadastrarTarefa = () => {
  const novaTarefa = {
    titulo: estado.tarefaTemp,
    finalizada: false
  }
  estado.tarefas.push(novaTarefa);
  estado.tarefaTemp = '';
}

</script>

<template>

  <div class="container">
    <header class="bg-light p-5 mb-4 mt-4 rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>
        Você possui {{ getTarefasPendentes().length }} tarefas pendentes
      </p>
    </header>    

    <form @submit.prevent="cadastrarTarefa">
    <div class="row">
      <div class="col">
        <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required type="text" placeholder="Digite a descrição da tarefa" class="form-control">
      </div>
      <div class="col-md-2">
        <button type="submit" class="btn btn-primary">Cadastrar</button>
      </div>
      <div class="col-md-2">
        <select @change="evento => estado.filtro = evento.target.value" class="form-control">
          <option value="todas">Todas as tarefas</option>
          <option value="pendentes">Tarefas pendentes</option>
          <option value="finalizadas">Tarefas finalizadas</option>
        </select>
      </div>
    </div>
  </form>
  <ul class="list-group mt-4">

    <li class="list-group-item" v-for="tarefa in filtarTarefas()">

      <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox" >
      <label :class=" { line: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">
        {{ tarefa.titulo }}
      </label>

    </li>

  </ul>
  </div>

</template>

<style scoped>

  .line {
    text-decoration: line-through;  
  }

</style>

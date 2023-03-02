<script setup>
import { reactive } from "vue";
import Cabecalho from "./components/Cabecalho.vue";
import Formulario from "./components/Formulario.vue";
import ListaDeTarefas from "./components/ListaDeTarefas.vue";

const estado = reactive({
  filtro: "todas",
  tarefaTemp: "",
  tarefas: [
    {
      titulo: "Estudar TypeScript",
      finalizada: false,
    },
    {
      titulo: "Estudar Node.js",
      finalizada: false,
    },
    {
      titulo: "Estudar Ingles",
      finalizada: true,
    },
  ],
});

const getTarefasPendentes = () => {
  return estado.tarefas.filter((tarefa) => !tarefa.finalizada); //itera sobre cada item do array, e retorna o valor pedido (tarefas finalizadas);
};

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter((tarefa) => tarefa.finalizada);
};

const getTarefasFiltradas = () => {
  const { filtro } = estado;

  switch (filtro) {
    case "pendentes":
      return getTarefasPendentes();
    case "finalizadas":
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;
  }
};

const cadastrarTarefa = () => {
  const novaTarefa = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  };
  estado.tarefas.push(novaTarefa);
  estado.tarefaTemp = "";
};
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :editar-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastar-tarefa="cadastrarTarefa"/>
    <ListaDeTarefas :condicao="getTarefasPendentes().length > 0" :tarefas="getTarefasFiltradas()"/>
  </div>
</template>
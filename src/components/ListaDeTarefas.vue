<script setup>
    const props = defineProps(['tarefas', 'condicao'])
</script>

<template>
  <ul v-if="condicao" class="list-group mt-4">
    <li class="list-group-item" v-for="tarefa in props.tarefas">
      <input @change="(evento) => (tarefa.finalizada = evento.target.checked)" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox" />
      <label :class="{ line: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">
        {{ tarefa.titulo }}
      </label>
    </li>
  </ul>
  <span v-else>Nenhuma tarefa pendente</span>
</template>


<style scoped>
  .line {
    text-decoration: line-through;
  }

</style>

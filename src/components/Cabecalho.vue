<script setup>
const props = defineProps(["tarefasPendentes"]);
</script>

<template>
  <header class="Bgcolor p-5 mb-4 mt-4 rounded-3">
    <h1 class="textColor">Minhas Tarefas</h1>
    <p class="textColor">Você possui {{ props.tarefasPendentes }} tarefas pendentes</p>
  </header>
</template>

<style scoped>

  .Bgcolor {
    background-color: #42b883;
  }

  .textColor {
    color: #fff;
  }

</style>





<script setup>
  const props = defineProps(['cadastarTarefa', 'tarefaTemp', 'trocarFiltro', 'editarTarefaTemp'])
</script>

<template>
  <form @submit.prevent="props.cadastarTarefa">
    <div class="row">
      <div class="col">
        <input :value="props.tarefaTemp" @change="props.editarTarefaTemp" required type="text" placeholder="Digite a descrição da tarefa" class="form-control" />
      </div>
      <div class="col-md-2">
        <button type="submit" class="btn">Cadastrar</button>
      </div>
      <div class="col-md-2">
        <select @change="props.trocarFiltro" class="form-control">
          <option value="todas">Todas as tarefas</option>
          <option value="pendentes">Tarefas pendentes</option>
          <option value="finalizadas">Tarefas finalizadas</option>
        </select>
      </div>
    </div>
  </form>
</template>

<style scoped>

  button {
    background-color: #42b883;
    border-color: #42b883;
    color: #fff;
  }

  button:hover {
    background-color: #0ee986;
  }
</style>



<script setup>
const props = defineProps([
  'cadastrarTarefa',
  'novoTitulo',
  'trocarFiltro',
  'editarTarefa',
]);
</script>

<template>
  <form @submit.prevent="props.cadastrarTarefa">
    <div class="row">
      <div class="col">
        <input
          :value="props.novoTitulo"
          @change="props.editarTarefa"
          type="text"
          placeholder="Digite a descrição da tarefa"
          class="form-control"
          required
        />
      </div>
      <div class="col-md-2">
        <button type="submit" class="btn btn-primary">Cadastrar</button>
      </div>
      <div class="col-md-2">
        <select @change="props.trocarFiltro" class="form-control">
          <option value="">Todas as tarefas</option>
          <option value="pendentes">Tarefas pendentes</option>
          <option value="finalizadas">Tarefas finalizadas</option>
        </select>
      </div>
    </div>
  </form>
</template>

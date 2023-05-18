<script setup>
import { reactive } from 'vue';

const estado = reactive({
  filtro: 'todas',
  tarefas: [
    {
      titulo: 'Estudar ES6',
      concluida: false,
    },
    {
      titulo: 'Estudar ReactJS',
      concluida: true,
    },
    {
      titulo: 'Trabalhar',
      concluida: false,
    },
  ],
});

const pegarTarefasPendentes = () => {
  return estado.tarefas.filter(({ concluida }) => !concluida);
};

const pegarTarefasFinalizadas = () => {
  return estado.tarefas.filter(({ concluida }) => concluida);
};

const pegarTarefasFiltradas = () => {
  const { filtro } = estado;

  switch (filtro) {
    case 'pendentes':
      return pegarTarefasPendentes();

    case 'finalizadas':
      return pegarTarefasFinalizadas();

    default:
      return estado.tarefas;
  }
};
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>Você possui {{ pegarTarefasPendentes().length }} tarefas pendentes</p>
    </header>
    <form>
      <div class="row">
        <div class="col">
          <input
            type="text"
            placeholder="Digite a descrição da tarefa"
            class="form-control"
          />
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select
            @change="({ target }) => (estado.filtro = target.value)"
            class="form-control"
          >
            <option value="todas">Todas as tarefas</option>
            <option value="pendentes">Tarefas pendentes</option>
            <option value="finalizadas">Tarefas finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li v-for="tarefa in pegarTarefasFiltradas()" class="list-group-item">
        <input
          @change="({ target }) => (tarefa.concluida = target.checked)"
          type="checkbox"
          :checked="tarefa.concluida"
          :id="tarefa.titulo"
        />
        <label
          :for="tarefa.titulo"
          :class="{ done: tarefa.concluida }"
          class="ms-3"
          for=""
          >{{ tarefa.titulo }}</label
        >
      </li>
    </ul>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>

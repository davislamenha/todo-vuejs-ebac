<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';

const estado = reactive({
  filtro: 'todas',
  novoTitulo: '',
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

const cadastrarTarefa = () => {
  const { novoTitulo, tarefas } = estado;
  const novaTarefa = {
    titulo: novoTitulo,
    concluida: false,
  };
  tarefas.push(novaTarefa);
  estado.novoTitulo = '';
};
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="pegarTarefasPendentes().length" />
    <Formulario
      :cadastrar-tarefa="cadastrarTarefa"
      :novo-titulo="estado.novoTitulo"
      :trocar-filtro="({ target }) => (estado.filtro = target.value)"
      :editar-tarefa="({ target }) => (estado.novoTitulo = target.value)"
    />
    <ListaDeTarefas
      :tarefas="pegarTarefasFiltradas()"
      :filtro="estado.filtro"
    />
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>

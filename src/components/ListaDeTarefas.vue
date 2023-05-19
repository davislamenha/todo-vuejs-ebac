<script setup>
const props = defineProps(['tarefas', 'filtro']);
</script>

<template>
  <ul v-if="props.tarefas.length" class="list-group mt-4">
    <li v-for="tarefa in props.tarefas" class="list-group-item">
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
  <span class="d-block mt-4" v-else>Não há tarefas {{ props.filtro }}</span>
</template>

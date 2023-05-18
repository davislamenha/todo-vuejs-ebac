<script setup></script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>Você possui 7 tarefas pendentes</p>
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
          <select class="form-control">
            <option value="todas">Todas as tarefas</option>
            <option value="pendentes">Tarefas pendentes</option>
            <option value="finalizadas">Tarefas finalizadas</option>
          </select>
        </div>
      </div>
    </form>
  </div>
</template>

<style scoped></style>

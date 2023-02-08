<template>
        <Cadastro @aoSalvarTarefa="salvarTarefa" />
        <!-- Lista de tarefas -->
        <div class="lista">
          <Tarefa v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa" />
          <Box v-if="listaVazia">
            Sem tarefas
          </Box>
        </div>
  </template>
  
  <script lang="ts">
  import { defineComponent } from 'vue';
  import Cadastro from '../components/Formulario.vue';
  import Tarefa from '../components/Tarefa.vue';
  import Box from '../components/Box.vue';
  import ITarefa from '../interfaces/ITarefa';
  
  export default defineComponent({
    name: 'App',
    components: {
      Cadastro,
      Tarefa,
      Box
    },
    data() {
      return {
        tarefas: [] as ITarefa[]
      }
    },
    computed: {
      listaVazia(): boolean {
        return this.tarefas.length === 0
      }
    },
    methods: {
      salvarTarefa(tarefa: ITarefa) {
        this.tarefas.push(tarefa)
      }
    }
  });
  </script>

<template>
  <main class="columns is-gapless is-multiline" :class="{'modo-escuro': modoEscuroAtivo }">
    <div class="column is-2">
      <BarraLateral @aoTemaAlterado="trocarTema"/>
    </div>
    <div class="column is-10 conteudo">
      <Formulario @aoSalvarTarefa="salvarTarefa" />
      <div class="lista">
        <Tarefa v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa" @ao-apagar-tarefa="apagarTarefa(index)"/>
        <Box v-if="listaEstaVazia">Você não está muito produtivo hoje :(</Box>
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue';
import Formulario from './components/Formulario.vue';
import Box from './components/Box.vue';
import Tarefa from './components/Tarefa.vue'
import ITarefa from './interfaces/ITarefa';

export default defineComponent({
  name: 'App',
  components: {
    BarraLateral,
    Formulario,
    Tarefa,
    Box
  },

  data() {
    return {
      tarefas: [] as ITarefa[],
      modoEscuroAtivo: true,
    }
  },
  methods: {
    salvarTarefa(tarefa : ITarefa) {
      this.tarefas.push(tarefa)
    },
    trocarTema(modoEscuroAtivo: boolean) {
      this.modoEscuroAtivo = modoEscuroAtivo;

    },
    apagarTarefa(indice: number) {
      this.tarefas.splice(indice, 1);
    }
  },
  computed: {
    listaEstaVazia() : boolean {
      return this.tarefas.length === 0
    }
  }
});
</script>

<style>
  .lista {
    padding: 10px;
  }

  main {
    --bg-primario: #fff;
    --txt-primario: #000
  }

  main.modo-escuro {
    --bg-primario: #2b2d42;
    --txt-primario: #ddd;
  }

  .conteudo {
    background-color: var(--bg-primario);
  }
</style>

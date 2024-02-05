<script lang="ts">
    import type IReceita from '@/interfaces/IReceita';
    import { obterReceitas } from '@/http/index';
    import type { PropType } from 'vue';
    export default {
  data() {
    return {
      receitas: [] as IReceita[],
    };
  },
  methods: {
    async fetchData() {
      try {
        this.receitas = await obterReceitas('categoria');
      } catch (error) {
        console.error(error);
      }
    },
  },
  mounted() {
    this.fetchData();
  },
};

</script>

<template>
    <h2>Receitas</h2>
    <div class="receitas-container">
        <div class="receitas-card" v-for="receita in receitas" :key="receita.nome">
          <article class="receita">
            <header class="receita-titulo">
              <img :src="`/imagens/receitas/${receita.imagem}`" alt="" class="receita-imagem">
              <h3>{{ receita.nome }}</h3>
            </header>
          </article>
        </div>
    </div>
  </template>
  
  <style scoped>

.receitas-container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-between;
  gap: 2rem;
}

.receitas-card {
  flex: 1 0 20%; 
  max-width: 20%;
}

.receita {
  width: 80%;
  padding: 1rem;
  border-radius: 1rem;
  background: var(--branco, #FFF);
  box-shadow: 4px 4px 10px 0px rgba(68, 68, 68, 0.05);
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center; 
  justify-content: center; 
  gap: 2rem;
  margin-bottom: 2rem;
}

.receita-titulo {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center; 
  gap: 0.5rem;
}

.receita-imagem {
  width: 15rem; 
  max-width: 100%; 
  max-height: 100%; 
}

</style>
<script lang="ts">
import ButtonSearchRecipe from './ButtonSearchRecipe.vue';
import Footer from './Footer.vue';
import SelectIngredients from './SelectIngredients.vue';
import ShowRecipes from './ShowRecipes.vue';
import Tag from './Tag.vue';
import YourList from './YourList.vue';

type Page = 'SelectIngredients' | 'ShowRecipes'

export default {
    data() {
        return {
            ingredientes: [] as string[],
            conteudo: 'SelectIngredients' as Page
        };
    },
    methods: {
      adicionarIngrediente(ingrediente: string) {
        this.ingredientes.push(ingrediente)
      },
      removerIngrediente(ingrediente: string) {
        this.ingredientes = this.ingredientes.filter(iLista => ingrediente !== iLista);
      },
      goToShowRecipes(page: Page) {
        this.conteudo = page;
      }
    },
    components: { SelectIngredients, Tag, YourList, Footer, ButtonSearchRecipe, ShowRecipes },
}
</script>

<template>
    <main class="conteudo-principal">

        <YourList :ingredientes="ingredientes" />

        <KeepAlive>
          <SelectIngredients v-if="conteudo === 'SelectIngredients'"
          @adicionar-ingrediente="adicionarIngrediente"
          @remover-ingrediente="removerIngrediente"
          @search-recipe="goToShowRecipes('ShowRecipes')"
          />
          <ShowRecipes v-if="conteudo === 'ShowRecipes'" @voltar="conteudo = 'SelectIngredients'" />
        </KeepAlive>
    </main>

    <Footer />


</template>

<style scoped>

.conteudo-principal {
  padding: 6.5rem 7.5rem;
  border-radius: 3.75rem 3.75rem 0rem 0rem;
  background: var(--creme, #FFFAF3);
  color: var(--cinza, #444);

  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5rem;
}

@media only screen and (max-width: 1300px) {
  .conteudo-principal {
    padding: 5rem 3.75rem;
    gap: 3.5rem;
  }
}

@media only screen and (max-width: 767px) {
  .conteudo-principal {
    padding: 4rem 1.5rem;
    gap: 4rem;
  }
}

</style>

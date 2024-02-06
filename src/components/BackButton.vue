<script lang="ts">
    export default {}
</script>

<template>
    <button class="botao-voltar" @click="$emit('voltar')">
        Editar Lista
    </button>
</template>

<style scoped>
    .botao-voltar {
        background: #ff8800;
        color: var(--branco, #ffffff);
        padding: 1rem 2rem;
        border: none;
        border-radius: 1rem;
        font-size: 1.5rem;
        cursor: pointer;
    }
</style>
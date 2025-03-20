<script lang="ts">
import type { PropType } from "vue";
import IReceita from "@/interfaces/IReceita";

export default {
  props: {
    receita: { type: Object as PropType<IReceita>, required: true },
  },
};
</script>

<template>
  <article class="categoria">
    <header class="categoria__cabecalho">
      <img
        :src="`/imagens/receitas/${receita.imagem}`"
        alt=""
        class="categoria__imagem"
      />

      <h2 class="paragrafo-lg categoria__nome">
        {{ receita.nome }}
      </h2>
    </header>
  </article>
</template>

<style scoped>
.categoria {
  width: 19.5rem;
  padding: 1rem;
  border-radius: 1rem;
  background: var(--branco, #fff);
  box-shadow: 4px 4px 10px 0px rgba(68, 68, 68, 0.05);
  height: 100%;

  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
}

.categoria__cabecalho {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
}

.categoria__imagem {
  width: 3.5rem;
}

.categoria__nome {
  text-align: center;
  color: var(--verde-medio, #3d6d4a);
  font-weight: 700;
}

.categoria__ingredientes {
  display: flex;
  justify-content: center;
  gap: 0.5rem;
  flex-wrap: wrap;
}
</style>

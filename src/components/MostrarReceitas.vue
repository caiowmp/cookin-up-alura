<script lang="ts">
import { obterReceitas } from "@/http/index";
import type IReceita from "@/interfaces/IReceita";
import BotaoPrincipal from "./BotaoPrincipal.vue";
import CardReceita from "./CardReceita.vue";

export default {
  data() {
    return {
      receitas: [] as IReceita[],
      texto:
        "Vejas as opções de receitas que encontramos por aí com os ingredientes que você tem!",
    };
  },
  async created() {
    this.receitas = await obterReceitas();

    if (this.receitas.length === 0)
      this.texto =
        "Ops, não encontramos resultados para sua combinação. Vamos tentar de novo?";
  },
  emits: ["editarLista"],
  components: { BotaoPrincipal, CardReceita },
};
</script>

<template>
  <section class="selecionar-ingredientes">
    <h1 class="cabecalho titulo-ingredientes">Receitas</h1>

    <p>Resultados encontrados: {{ receitas.length }}</p>

    <p class="paragrafo-lg instrucoes">
      {{ texto }}
    </p>

    <img
      src="../assets/imagens/sem-receitas.png"
      alt=""
      v-if="receitas.length === 0"
    />

    <ul class="categorias">
      <li v-for="receita in receitas" :key="receita.nome">
        <CardReceita :receita="receita" />
      </li>
    </ul>

    <BotaoPrincipal
      texto="Editar lista"
      @click="$emit('editarLista')"
    ></BotaoPrincipal>
  </section>
</template>

<style scoped>
.selecionar-ingredientes {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.titulo-ingredientes {
  color: var(--verde-medio, #3d6d4a);
  display: block;
  margin-bottom: 1.5rem;
}

.instrucoes {
  margin-bottom: 2rem;
}

.categorias {
  margin-bottom: 1rem;
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.dica {
  align-self: flex-start;
  margin-bottom: 3.5rem;
}

@media only screen and (max-width: 767px) {
  .dica {
    margin-bottom: 2.5rem;
  }
}
</style>

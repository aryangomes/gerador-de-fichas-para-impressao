<template>
  <div
    class="ficha text-center text-weight-bolder"
    :style="estiloDaFicha"
  >
    {{ texto }}
  </div>
</template>

<script lang="ts">
export default {
  name: "Ficha",
  data() {
    return {};
  },
  props: {
    texto: {
      type: String,
      default: function () {
        return "Ficha";
      },
    },
    configuracoes: {
      default: function () {
        return {
          tamanhoFicha: 4,
          espessuraBorda: 0.15,
          alturaTexto: 3,
          tamanhoTexto: 1,
        };
      },
    },
  },

  computed: {
    estiloDaFicha() {
      return (
        `height: ${this.configuracoes.tamanhoFicha}cm;` +
        `width:  ${this.configuracoes.tamanhoFicha}cm;` +
        `font-size: ${this.configuracoes.tamanhoTexto}cm;` +
        `border: ${this.configuracoes.espessuraBorda}cm solid black;` +
        `line-height:${this.configuracoes.alturaTexto}cm`
      );
    },
  },
};
</script>

<style>
.ficha {
  word-wrap: break-word;
  display: flex;
  justify-content: center;
  align-content: center;
  flex-direction: column;
}
</style>

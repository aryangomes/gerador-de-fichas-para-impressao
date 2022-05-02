<template>
  <div class="ficha" :style="style">
    <p class="text-center text-weight-bolder" style="font-size: 2cm;">
      {{ texto }}
    </p>
  </div>
</template>

<script lang="ts">
export default {
  name: "Ficha",
  data() {
    return {
      alturaFicha: 4,
      larguraFicha: 4,
      espessuraBorda: 3,
    };
  },
  props: {
    texto: {
      default: "Ficha",
    },
  },

  computed: {
    style() {
      return (
        `height: ${this.alturaFicha}cm;` +
        `width:  ${this.larguraFicha}cm;` +
        `border: ${this.espessuraBorda}px solid black;` +
        `line-height:${this.alturaFicha}cm`
      );
    },
  },
};
</script>

<style>
.ficha{
  margin: 0.01cm;
}
</style>

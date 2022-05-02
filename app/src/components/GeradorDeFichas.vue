<template>
  <div>
    <!-- <p>Total de Fichas: {{ totalDeFichas }}</p> -->
    <section>
    <div v-for="linha in totalDeLinhas" :key="linha">
      <div class="column inline" v-for="(ficha) in totalDeFichasPorLinha" :key="ficha">

        <Ficha id="impressao" :texto="gerarTextoParaImpressaoDaFicha(ficha, linha)"> </Ficha>
      </div>
    </div>
    </section>
  </div>
</template>

<script lang="ts">
import Ficha from "./Ficha.vue";
export default {
  name: "GeradorDeFichas",
  components: { Ficha },
  data () {
    return {
      valorFicha: 0,
      totalDeFichas: 50,
      totalDeFichasPorLinha: 5,


    };
  },
  computed: {
    totalDeLinhas () {
      return this.totalDeFichas / this.totalDeFichasPorLinha;
    },
    /*  totalDeFichasPorLinha() {
      return this.totalDeFichas / this.linhas;
    }, */
  },
  methods: {
    gerarTextoParaImpressaoDaFicha (ficha, linha) {
      return ficha + (this.totalDeFichasPorLinha * (linha - 1));
    }
  },

};
</script>
<style>
</style>

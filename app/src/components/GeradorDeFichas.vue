<template>
  <main>

    <section id="area-para-nao-imprimir">
      <q-form class="q-gutter-md">
        <div class="q-gutter-sm">
          <q-radio
            v-model="tipoDeTextoParaImpressaoNaFicha"
            val="numeros"
            label="Números"
          />
          <q-input
            v-model.number=totalDeLinhas
            label="Total de Linhas"
            type="number"
            step="1"
          />
          <q-input
            v-model.number=totalDeFichasPorLinha
            label="Total de Fichas por linha"
            type="number"
            step="1"
          />
          <q-radio
            v-model="tipoDeTextoParaImpressaoNaFicha"
            val="texto"
            label="Texto"
          />
        </div>
        <div
          v-if="imprimirTextoNaFicha"
          class="q-gutter-md"
        >
          <q-input
            v-model="textoParaExibirNaFicha"
            label="Texto"
          />
        </div>

      </q-form>
      <div class="q-pa-md q-gutter-sm">
        <q-btn
          label="Configurações da Ficha"
          color="primary"
          @click="abrirTelaDeConfiguracaoDaFicha = true"
        />
        <q-btn
          color="amber"
          glossy
          label="Imprimir"
          @click="gerarImpressao()"
        />

        <q-dialog v-model="abrirTelaDeConfiguracaoDaFicha">
          <q-card>
            <q-card-section>
              <div class="text-h6">Configurações da Ficha</div>
            </q-card-section>

            <q-card-section class="q-pt-none">
              <q-form class="q-gutter-md">
                <div class="q-pa-md">
                  <q-input
                    v-model.number="configuracoes.tamanhoFicha"
                    type="number"
                    label="Tamanho da Ficha"
                    style="max-width: 200px"
                    suffix="cms"
                    step="0.1"
                  />
                </div>

                <div class="q-pa-md">
                  <q-input
                    v-model.number="configuracoes.espessuraBorda"
                    type="number"
                    label="Espessura da borda"
                    style="max-width: 200px"
                    suffix="cms"
                    step="0.05"
                  />
                </div>

                <div class="q-pa-md">
                  <q-input
                    v-model.number="configuracoes.tamanhoTexto"
                    type="number"
                    label="Tamanho do Texto"
                    style="max-width: 200px"
                    suffix="cms"
                    step="0.1"
                  />
                </div>

                <div class="q-pa-md">
                  <q-input
                    v-model.number="configuracoes.alturaTexto"
                    type="number"
                    label="Altura do texto"
                    style="max-width: 200px"
                    suffix="cms"
                    step="0.1"
                  />
                </div>
              </q-form>
            </q-card-section>

            <q-card-actions align="right">
              <q-btn
                @click="resetarConfiguracaoDaFicha()"
                label="RESETAR CONFIGURAÇÕES DA FICHA"
                color="warning"
              />
              <q-btn
                label="FECHAR"
                color="primary"
                v-close-popup
              />
            </q-card-actions>
          </q-card>
        </q-dialog>
      </div>
    </section>
    <section>
      <div>
        <p>Total de Fichas: {{ totalDeFichas }}</p>
      </div>
    </section>
    <section id="area-para-impressao">
      <div
        v-for="linha in totalDeLinhas"
        :key="linha"
      >

        <div
          class="column inline"
          v-for="ficha in totalDeFichasPorLinha"
          :key="ficha"
        >
          <Ficha
            :configuracoes="configuracoes"
            :texto="gerarNumeroParaImpressaoDaFicha(ficha, linha)"
            v-if="imprimirNumerosNaFicha"
          >
          </Ficha>

          <Ficha
            :configuracoes="configuracoes"
            :texto="textoParaExibirNaFicha"
            v-if="imprimirTextoNaFicha"
          >
          </Ficha>
        </div>

      </div>
    </section>
  </main>
</template>

<script lang="ts">
import Ficha from "./Ficha.vue";
export default {
  name: "GeradorDeFichas",
  components: { Ficha },
  data() {
    return {
      totalDeLinhas: 10,
      totalDeFichasPorLinha: 5,
      tipoDeTextoParaImpressaoNaFicha: "numeros",
      textoParaExibirNaFicha: "Ficha",
      abrirTelaDeConfiguracaoDaFicha: false,
      configuracoes: {},
    };
  },
  mounted() {
    this.resetarConfiguracaoDaFicha();
  },
  computed: {
    totalDeFichas() {
      return this.totalDeLinhas * this.totalDeFichasPorLinha;
    },

    imprimirNumerosNaFicha() {
      return this.tipoDeTextoParaImpressaoNaFicha === "numeros";
    },

    imprimirTextoNaFicha() {
      return this.tipoDeTextoParaImpressaoNaFicha === "texto";
    },
  },
  methods: {
    gerarNumeroParaImpressaoDaFicha(ficha, linha) {
      return "" + (ficha + this.totalDeFichasPorLinha * (linha - 1));
    },
    gerarImpressao() {
      window.print();
    },
    resetarConfiguracaoDaFicha() {
      return (this.configuracoes = {
        tamanhoFicha: 4,
        alturaTexto: 4,
        espessuraBorda: 0.15,
        tamanhoTexto: 3,
      });
    },
  },
};
</script>
<style>
section {
  margin-left: 0.5cm;
}
@media print {
  @page {
    margin: 1cm 0 1cm 0;
    size: A4 portrait;
  }
  #area-para-nao-imprimir {
    display: none;
  }
  #area-para-impressao {
    display: block;
  }

  body * {
    visibility: hidden;
  }
  #area-para-impressao,
  #area-para-impressao * {
    visibility: visible;
  }
  #area-para-impressao {
    left: 0;
    top: 0;
  }
}
</style>

<template>
  <div>
    <GeradorDeFichas> </GeradorDeFichas>
  </div>
</template>

<script>
import GeradorDeFichas from "src/components/GeradorDeFichas.vue";
export default {
  name: "PageIndex",
  components: { GeradorDeFichas },
};
</script>
<style>
* {
  margin: 0;
  padding: 0;
}
@media print {
  @page {
    margin: 0;
    size: A4 portrait;
  }
  body {
    margin-top:0.5cm ;
    margin-left:1cm ;
  }
}
</style>

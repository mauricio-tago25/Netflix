<template>
  <div class="gui-card">
    <div class="gui-card__media">
      <!--<img class="gui-card__img" v-bind:src="imagem" alt=""/>-->
      <iframe class="gui-card__img" v-bind:src="url" allowfullscreen></iframe>
    </div>
  </div>
</template>

<script>
  export default {
    name: "Filme",
    props: ['nomeFilme', 'url'],
    data() {
      return {
        efeito: null
      }
    },
    methods: {
      clickEfeito() {
        this.efeito = 'transform: scale(1.9); margin-right: 110px';
      },
      removeClickEfeito() {
        this.efeito = null;
      }
    }
  }
</script>

<style scoped>

</style>

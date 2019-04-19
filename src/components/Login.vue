<template>
  <div>
    <b-form @submit="onSubmit" @reset="onReset" v-if="show">

      <b-form-group id="input-group-1" label="Nome:" label-for="input-1">
        <b-form-input
          id="input-1"
          v-model="form.nome"
          required
          placeholder="Digite seu nome"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Senha:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.senha"
          required
          type="password"
          placeholder="Digite sua senha"
        ></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary">Enviar</b-button>
      <b-button type="reset" variant="danger">Limpar</b-button>
    </b-form>

  </div>
</template>

<script>
  export default {
    data() {
      return {
        form: {
          nome: '',
          senha: ''
        },
        show: true
      }
    },
    methods: {
      onSubmit(evt) {
        evt.preventDefault();
        alert(JSON.stringify(this.form))
      },
      onReset(evt) {
        evt.preventDefault();
        // Reset form values
        this.form.nome = '';
        this.form.senha = '';
        // Trick to reset/clear native browser form validation state
        this.show = false;
        this.$nextTick(() => {
          this.show = true
        })
      }
    }
  }
</script>

<style scoped>

</style>

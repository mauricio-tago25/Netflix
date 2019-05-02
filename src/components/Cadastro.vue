<template>

  <div class="login">

    <b-form class="formulario" c @submit="cadastro">

      <h1 id="titulo">Netflix</h1>
      <h2 id="subtitulo">Tela de Cadastro</h2>

      <div v-show="msgSucesso">
        <b-alert show variant="primary" dismissible>Cadastrado com sucesso!</b-alert>
      </div>

      <div v-show="msgErro">
        <b-alert show variant="danger" dismissible>Usuário já cadastrado!</b-alert>
      </div>

      <b-form-group id="input-group-1" label="Nome:" label-for="input-1">
        <b-form-input
          id="input-1"
          v-model="usuario.nome"
          type="text"
          required
          placeholder="Digite o usuário"
        ></b-form-input>
      </b-form-group>


      <b-form-group id="input-group-2" label="Senha:" label-for="input-2">
        <b-form-input
          id="input-2"
          type="password"
          v-model="usuario.senha"
          required
          placeholder="Insira a senha"
        ></b-form-input>
      </b-form-group>

      <div id="botao">
        <b-button type="submit" value="Cadastrado" variant="primary" v-on:click="cadastro()">Cadastrar
        </b-button>
        <a href="/">
          <b-button variant="danger">Login</b-button>
        </a>
      </div>

    </b-form>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        usuario: {
          id: '',
          nome: '',
          senha: ''
        },
        cadastroUsuario: null,
        msgSucesso: false,
        msgErro:false,
        usuariosCadastrados: []
      }
    },
    methods: {
      cadastro(evt) {
        this.$http.get('http://localhost:3000/clientes').then(response => {
          this.usuariosCadastrados = response.body;
        });

        var cadastrado = false;

        for (var i in this.usuariosCadastrados) {
          if (this.usuario.nome === this.usuariosCadastrados[i].nome) {
            cadastrado = true;
            this.msgErro = true;
          }
        }

        if (cadastrado === false) {
          evt.preventDefault();
          this.$http.post('http://localhost:3000/clientes', this.usuario).then(response => {
            this.cadastroUsuario = response.body;
            this.msgSucesso = true;
            this.atualizar()
          })
        }
      },
      atualizar() {
        this.$http.get('http://localhost:3000/clientes').then(response => {
          this.usuariosCadastrados = response.body;
        });
      }
    },
    created() {
      this.$http.get('http://localhost:3000/clientes').then(response => {
        this.usuariosCadastrados = response.body;
      });
    },

  }
</script>

<style scoped>
  .login {
    background-image: url("http://cartoondistrict.com/wp-content/uploads/2015/02/Cute-Minion-Wallpapers-HD-for-Desktop-8.jpg");
    background-repeat: no-repeat;
    width: 100%;
    height: 100%;
    position: absolute;
    background-size: 100%;
  }

  .formulario {
    margin: 150px 500px 0 500px;
    color: white;
  }

  #botao {
    text-align: center;
  }

  #titulo {
    color: gainsboro;
    font-size: 50px;
    text-align: center;
    margin-bottom: 20px;
  }

  #subtitulo {
    color: gainsboro;
    font-size: 25px;
    text-align: center;
    margin-bottom: 20px;
  }
</style>

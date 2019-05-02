<template>

  <div class="login">

    <b-form class="formulario">

      <h1 id="titulo">Netflix</h1>
      <h2 id="subtitulo">Tela de Login</h2>

      <div v-show="msg">
        <b-alert show variant="danger" dismissible>Usuário ou senha incorreto!</b-alert>
      </div>

      <b-form-group label="Nome:" label-for="inputNome">
        <b-form-input
          id="inputNome"
          placeholder="Digite seu nome"
          v-model="nome"
        ></b-form-input>
      </b-form-group>

      <b-form-group label="Senha:" label-for="inputSenha">
        <b-form-input
          id="inputSenha"
          type="password"
          placeholder="Digite sua senha"
          v-model="senha"
        ></b-form-input>
      </b-form-group>

      <div id="botao">
        <b-button variant="success" @click="login()">Entrar</b-button>
        <a href="#/cadastro">
          <b-button variant="info">Cadastrar-se</b-button>
        </a>
      </div>
    </b-form>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        users: [],
        id: "",
        nome: "",
        senha: "",
        msg: false
      }
    },
    created() {
      this.$http.get('http://localhost:3000/clientes').then(response => {
        this.users = response.body;
        console.log(this.users);
      })
    },
    methods: {
      login() {
        let nome = this.nome;
        let senha = this.senha;

        const compararLoginDosUsuarios = (verificaUsuario) => {
          return verificaUsuario.nome === nome && verificaUsuario.senha === senha;
        };

        var usuarioCadastrado = this.users.filter(compararLoginDosUsuarios);

        if (usuarioCadastrado.length === 1) {
          window.location.href = "#/filmes";
        } else {
          this.msg = true;
        }
      }
    }
  }
</script>

<style scoped>
  .login {
    background-image: url("https://www.hellomoto.com.br/wp-content/uploads/2018/05/hellocinemaheader.png");
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
    color: #2e3133;
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

<template>
  <div class="title"> Questões Vue.js 3 </div>
  <div class="info">
    Abaixo estão três componentes cuja estrutura apresentada deve ser modificada a fim
    de replicar as funcionalidades neles pedidas. Seu código deve contemplar todas as
    funcionalidades requisitadas, bem como as mudanças visuais a fim de tornar a página esteticamente mais agradável e adequada a experiência do usuário.
  </div>
  <Senha />
  
  <DropDown ref="dd" :opcoesDD="opcoesSelect" v-model:parent-op="parentOp"/>
  <div class="results">
    <h1>{{ parentOp }}</h1>
  </div>
  <Lista :dados="dadosLista" @mudancaEmitida="mudancaLista" />
  <h1 class="results"> {{dadosN}}</h1>
  <br />
  <div class="info msg">
    Em caso de dúvida entre em contato pelo email <a href="mailto:mardt@usp.br">mardt@usp.br</a>.
    <br />
    Boa sorte e bom trabalho!
    <br />
    (⌒‿⌒)
  </div>
</template>

<script>
  import Lista from './components/Lista.vue';
  import Senha from './components/Senha.vue';
  import DropDown from './components/DropDown.vue';

  export default {
    name: 'App',
    components: {
      Senha,
      Lista,
      DropDown
    },
    data() {
      return {
        dadosLista: [{
          id: 1,
          op1: "1.1",
          op2: "1.2",
        },{
          id: 2,
          op1: "2.1",
          op2: "2.2",
        }],
        opcoesSelect: [
          "Opção 1",
          "Opção 2",
          "Opção 3",
          "Opção 4",
          "Opção 5",
          "Opção 6",
          "Opção 7",
        ],
        parentOp: ["parent's array"],
        dadosN: []
      };
    },
    methods: {
      mudancaLista(veio) {
        console.log('Lista recebida!')
        // Exiba a lista editada
        this.dadosN = veio;
      }
    },
    mounted() {
    }
  }
</script>

<style>
 #app {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
 }

 .title {
   width: 100%;
   text-align: center;
   font-size: 2rem;
   font-weight: bolder;
   margin-bottom: 20px;
 }

 .question-title {
   font-size: 1.5rem;
   font-weight: bold;
 }

 .results{
    display: inline-block;
    width: 100%;
    text-align: center;
    margin: 0 auto;
}

 .question-text {
   font-size: 1rem;
   font-style: italic;
   margin-bottom: 5px;
   text-align: justify;
 }

 .question-text > tt {
     font-style: normal;
 }

 .info {
   font-size: 1.1rem;
   margin-bottom: 10px;
   text-align: justify;
 }

 .msg {
   text-align: center;
 }
</style>

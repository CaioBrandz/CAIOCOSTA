<template>
    <div class="question-title">Questão 2</div>
    <div class="question-title">Dropdown:</div>
    <div class="question-text">
        Transforme a estrutura dada em um seletor dropdown (como um <tt>&#60;select/&#62;</tt>)
        a partir das opções dadas em <tt>:opcoesDD</tt>, indicando a opção atualmente selecionada
        no texto do seletor e visualmente na lista de opções. A opção padrão deve ser inicialmente
        a primeira opção dada na lista. Crie também uma função que retorne a opção selecionada no
        formato <tt>[ texto, idx ]</tt> ('texto' sendo a opção em si, e 'idx' seu índice na lista)
        para leitura pelo componente pai.
    </div>

    <div class="dropdown" :class="{'down': estado}" @click.stop.prevent="isOpen = !isOpen"> {{ opcaoSelecionada }} 
        <div>▾</div> 
    </div>
    <ul :class="{'opcoes': estado}" v-show="isOpen">
        <li :class="{'active': verify(index)}" v-for="(opcao,index) in opcoesDD" v-bind:key="index" @click="modalContent(index)">{{opcao}}</li>
        <!-- OPÇÕES PASSADAS (INDICANDO A ATUAL SELECIONADA) -->
    </ul>
    <div class="results">
        <button @click="pass()">passar para o pai</button>
    </div>
</template>

<script>
    export default {
        name: "DropDown",
        props: {
            opcoesDD: Array,
            parentOp: Array,
        },
        emits: ['update:parentOp'],
        data() {
            return {
                opcaoSelecionada: this.opcoesDD[0],
                isOpen :false,
            };
        },
        computed: {
            estado() { return this.isOpen; },
            opcaoS(){
                return [this.opcaoSelecionada,this.opcoesDD.indexOf(this.opcaoSelecionada)];
            }
        },
        methods: {
            // Permitir ler dados...
            modalContent(index){
                this.opcaoSelecionada = this.opcoesDD[index];
                this.isOpen = false;      
            },
            verify(index){
                if(this.opcaoSelecionada == this.opcoesDD[index])
                    return true;
                else return false;
            },
            pass(){
                this.$emit('update:parentOp', this.opcaoS);
            }
        },
        // Atualizar dados com opções passadas...
    }
</script>

<style scoped>
 .dropdown {
     cursor: pointer;
     border: 1px solid #2c3e50;
     border-radius: 5px;
     width: 20%;
     display: flex;
     margin: 0 auto;
     padding: 5px;
     text-align: center;
     justify-content: space-between;
     border-width: 2px;
    border-image: linear-gradient(145deg,#5B42F3 50%,#00DDEB);
    border-image-slice: 1;
    min-width: 150px;
 }

.results{
    display: inline-block;
    width: 100%;
    text-align: center;
    margin: 2rem auto 0 auto;

}
 .opcoes {  
    left: 50%;
    transform: translate(-50%, 0px);
    position: absolute;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    grid-row-gap: 1.5em;
    grid-column-gap: 20px;
    padding: 20px;
    max-width: 620px;
    width: 85%;
    margin: 0 auto;
    text-align: center;
    list-style: none;
    color: rgba(66, 69, 243, 0.95);
    font-weight: 700;
    background: rgba( 255, 255, 255, 0.75 );
    box-shadow: 0 8px 32px 0 rgba( 31, 38, 135, 0.37 );
    backdrop-filter: blur( 5px );
    -webkit-backdrop-filter: blur( 5px );
    border-radius: 10px;
    border: 1px solid rgba( 255, 255, 255, 0.18 );
    animation: modal .5s;
 }
 .active::before, .opcoes > li:hover::before{
    content: '< ';
    display: inline-block;
    color: #00DDEB;
    font-weight: 700;
    opacity: 0.4;
    transform: translateX(-5px);
    animation-name: example;
    animation-duration: 2s;
    animation-iteration-count: infinite;
}

@keyframes example {
  0%   {}
  50% {opacity: 1;
    transform: translateX(-10px);}
}

.active::after, .opcoes > li:hover::after {
    content: ' >';
    display: inline-block;
    color: #00DDEB;
    font-weight: 700;
    opacity: 0.4;
    transform: translateX(5px);
    animation-name: example2;
    animation-duration: 2s;
    animation-iteration-count: infinite;
}
@keyframes example2 {
  0%   {}
  50% {opacity: 1;
    transform: translateX(10px);}
}
 .opcoes > li{
    padding: 10px 10px;
    border-radius: 8px;
    cursor: pointer;
 }

.results>button{
  background-image: linear-gradient(145deg,#5B42F3 50%,#00DDEB);
  border: none;
  border-radius: 8px;
  box-shadow: rgba(151, 65, 252, 0.2) 0 15px 30px -5px;
  color: #FFFFFF;
  font-size: 20px;
  padding: 19px 24px;
  text-decoration: none;
  cursor: pointer;
}

.results>button:hover {
  opacity: 0.8;
}

@keyframes modal {
	from{
		opacity: 0;
		transform: translate(-50%, -10px);
	}
	to{
		opacity:1;
		transform: translate(-50%, 0px);
	}
}


</style>

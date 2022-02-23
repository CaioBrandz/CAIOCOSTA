<template>
    <div class="question-title">Questão 1</div>
    <div class="question-title">Processamento de senha:</div>
    <div class="question-text">
        Crie funções de conferência para cada elemento necessário à entrada de senha
        (ao menos um caractere minúsculo, ao menos 8 caracteres, senhas iguais, etc...)
        e exiba os pontos conferidos apenas quando o usuário começar a digitar na caixa
        de texto.
    </div>

    <span v-if="errors.length" v-show="isFocused" class="validationBox">
        <p>Por favor, corrija o(s) seguinte(s) erro(s):</p>
        <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
        </ul>
    </span>
    
    <div class="form-group">
        <input v-model="senha" type="password" id="senha" placeholder="Insira sua senha..." required @keyup="checkForm();verify()" @focus="isFocused = true" @blur="isFocused = false"/>
        <label for="senha"> <span> Senha: </span> </label>
    </div>
    <div class="form-group">
        <input v-model="senhaConf" type="password" id="senhaConf" placeholder="Repita a senha..." required @keyup="verify()"/>
        <label for="senha"> <span> Repita a senha: </span> </label>   
    </div>

    <p v-show="isEqual" class="senha-err">As senhas estão diferentes!</p>


</template>

<script>
    export default {
        name: "Senha",
        data() {
            return {
                senha: "",
                senhaConf: "",
                isFocused: false,
                errors:[],
                isEqual: false,
            };
        },
        computed: {
            placeholder() {
                return true;
            },
        },
        methods: {
            conts(){
            var i=0, countU =0, countL =0, countC =0, countN =0;
            const alfa = /\W|_/;
                while (i <= this.senha.length){
                    var character = this.senha.charAt(i);
                    
                    if (character == character.toLowerCase() && character != character.toUpperCase()){
                        countL++;
                    }
                    if (character == character.toUpperCase() && character != character.toLowerCase()) {
                        countU++;
                    }
                    if (alfa.test(character)){
                        countC++;
                    }
                    if (isNaN(parseFloat(character)) == false){
                        countN++;
                    }
                    i++;
                }
                if (countU < 1){
                    this.errors.push('Falta caractere MAIUSCULO');
                }
                if (countL < 1){
                    this.errors.push('Falta caractere minusculo');
                }
                if (countC < 1){
                    this.errors.push('Falta caractere especial');
                }
                if (countN < 1){
                    this.errors.push('Falta numero');
                }
            },
            checkForm() {
                this.errors = [];
                if (!this.senha) {
                    this.errors = [];
                } 
                else{                   
                    if (this.senha.length < 8){
                        this.errors.push('Senha com menos de 8 caracteres');
                    }
                    this.conts();
                } 
                if (!this.errors.length) {
                    return true;
                }
            },
            verify(){
                if(this.senhaConf != this.senha)
                    this.isEqual = true;
                else this.isEqual = false;
            }
        },

    }
</script>

<style scoped>
.form-group {
    position: relative;
    padding: 15px 0;
    margin-top: 10px;
    width: 50%;
    display:flex;
    margin: 0 auto;
}

@media screen and (max-width: 800px) {
    .form-group {
        width: 90%;
    }
}

.form-group > label {
    position: absolute;
    top: 0;
    display: block;
    transition: 0.2s;
    font-size: 1rem;
    color: gray;
    margin: 5px 0px 5px 5px;
    padding: 0 8px;
    background-color: white;
}

.form-group > label > span {
    width: 100%;
}

.form-group > input {
    font-family: inherit;
    width: 100%;
    border: 2px solid gray;
    outline: 0;
    font-size: 1.3rem;
    color: #154c79;
    padding: 7px 12px;
    background: transparent;
    transition: border-color 0.2s;
}

input:placeholder-shown ~ label{
    font-size: 1.3rem;
    cursor: text;
    top: 20px;
  }

input::placeholder {
    color: transparent;

}
input:focus {
  padding-bottom: 6px;  
  font-weight: 700;
  border-width: 3px;
  border-image: linear-gradient(to right, #11998e,#38ef7d);
  border-image-slice: 1;
}

input:focus ~ label {
    position: absolute;
    top: 0;
    display: block;
    transition: 0.2s;
    font-size: 1rem;
    color: #11998e; 
    font-weight:700;   
    background-color: white;
}

.conferido {
    color: green !important;
}

.senha-err {
    color: red;
    text-align: center;
}

.validationBox{
    padding: 5px;
    position: absolute;
    left: 60%;
    transform: translate(-50%, -160px);
    width: calc(30% - 20px);
    min-width: 300px;
    color:rgb(235, 51, 51);
    background-color: white;
    border-radius: 15px;
    z-index: 5;
    font-size: 14px;
    box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;

}

@media screen and (max-width:576px){
    .validationBox{
        left: 50%;
        min-width: 240px;
        transform: translate(-50%, -200px);
    }
    .validationBox:after{
        left: 70%!important;
    }
}

.validationBox > p{
    text-align: center;
    font-weight: 700;
}

.validationBox>ul>li{
    list-style: none;
    text-decoration: none;
}

.validationBox:after{ /*Triangulo*/
    content: "";
    width: 0;
    height: 0;
    position: absolute;
    border-left: 20px solid transparent;
    border-right: 20px solid transparent;
    border-top: 20px solid white;
    bottom: -20px;
    left: 80%;
    box-shadow: rgba(50, 50, 93, 0.25) 0px 50px 100px -20px, rgba(0, 0, 0, 0.3) 0px 30px 60px -30px, rgba(10, 37, 64, 0.35) 0px -2px 6px 0px inset;
}

.validationBox>ul>li::before{
    content: '! ';
    font-size: 24px;
    display: inline-block;
    color: red;
    font-weight: 700;
    opacity: 1;
    transform: translateX(-5px);
    animation-name: example;
    animation-duration: 2s;
    animation-iteration-count: infinite;
}

  
</style>

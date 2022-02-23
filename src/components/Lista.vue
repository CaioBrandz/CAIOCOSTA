<template>
    <div class="question-title">Questão 3</div>
    <div class="question-title">Edição de entradas:</div>
    <div class="question-text">
        Modifique este componente para que exiba as entradas da lista de objetos (com a estrutura abaixo) cujas as propriedades devem ser inputs no componente <tt>div.entrada</tt>, atualizando
        seus valores no componente pai caso editadas. Cada objeto na lista deve pertencer ao seu próprio elemento. Exiba todos corretamente, exiba os indicadores corretos e repasse os dados ao componente pai ao se clicar no botão atualizar.
        <br />
        <pre class="json-example"><i>// Entrada:</i>
<code>{
    id: Number,
    op1: String,
    op2: String
}</code></pre>
    </div>

    Indicadores:
    <ul>
        <li v-if="placeholder">LISTA VAZIA</li>
        <li v-if="placeholder">MAIS DE 5 ELEMENTOS</li>
        <li v-if="placeholder">UMA OU MAIS ENTRADAS NÃO RESPEITA O FORMATO</li>
    </ul>

    <div class="entradas">
        <div class="entrada" v-for="(li,index) in lista" v-bind:key="index" >
            <div class="info"> 
                <h1>Index = {{index}}</h1>
                <h1>Id = {{li.id}}</h1>
                <h1>{{li}}</h1>
            </div>
            <div class="inputs">
                <label for="op1">Op1: </label>
                <input type="text" id="op1" :value="li.op1" @keyup="up2(index,$event.target.value)">
            </div>
            <div class="inputs">
                <label for="op2">Op2: </label>
                <input type="text" id="op2" :value="li.op2"  @keyup="up1(index,$event.target.value)" >
            </div>
        </div>
    </div>

    <button type="submit" @click="update" class="form-button" >Atualizar</button>
</template>

<script>
    export default {
        name: "Lista",
        props: {
            dados: {
                type: Array,
                required: true,
                mudancaEmitida: Array,
            },
            
        },
        emits: ['mudancaEmitida'],
        data() {
            return {
                lista: [...this.dados], // deve representar a lista dada
            };
        },
        watch: {},
        computed: {
            placeholder() { return true; },
        },
        methods: {
            up1(index,a) {
                console.log(index);
                this.lista.splice(index,1,{'id':this.lista[index].id,'op1':this.lista[index].op1,'op2':a});
            },
            up2(index,a) {
                console.log(index);
                this.lista.splice(index,1,{'id':this.lista[index].id,'op1':a,'op2':this.lista[index].op2});
            },
            update(){
                this.$emit('mudancaEmitida', this.lista);
            }
        }
    }
</script>

<style scoped>
 .form-button {
     font-size: 1.15rem;
     border-radius: 10px;
     border: 1px solid grey;
     background-color: #2c3e50;
     display: block;
     margin: 0 auto;
     padding: 5px;
     color: whitesmoke;
     cursor: pointer;
 }

 .entradas {
    width: 100%;
    display: flex;
    justify-content: space-evenly;
    flex-wrap: wrap;
 }

 .entrada {
    margin: 20px;
    min-width: 180px;
    width: 30%;
    padding: 20px;
    background-image: linear-gradient(315deg,#6111a3 0%,#f34242 200%);
    border: none;
    border-radius: 8px;
    box-shadow: rgba(151, 65, 252, 0.2) 0 15px 30px -5px;
    color: #FFFFFF;
    font-size: 20px;

 }
 .inputs>input{
     width: calc(40%);
    border: 2px solid white;
    border-radius: 8px;
    background-color: rgb(231, 231, 231);
    padding: 10px 5px;
    outline: 0;
    font-size: 1rem;
 }
 .inputs{
    margin: 1rem;
    display: flex;
    justify-content: center;
 }

 .info{
    text-align: center;
    font-size: 0.8rem;
 }

 .json-example {
     font-style: normal;
     background-color: lightgrey;
     border: 1px solid #2c3e50;
     padding: 5px;
 }

 .json-example > code {
     font-family: "Courier New", monospace !important;
 }
</style>

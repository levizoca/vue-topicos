<template>
  <div class="about">
    <h1>Anotação Page</h1>
  </div>
  <div id="cadastrar">
        <p>Texto: <input type="text" v-model="texto"/><button @click="doCadastrar">Cadastrar</button></p>
        <button @click="atualizar">Ok</button>
    </div>
  <div>
    <ul>
        <li v-for="(anotacao, index) in anotacoes" :key="index">{{anotacao.texto}}</li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';
import {mapState} from 'vuex';

export default {
    name: 'anotacaoView',
    data() {
        return {
            texto: '',
            anotacoes: [{texto: 'Teste'}, {texto: 'Teste2'}]
        }
    },
    computed: {
        ...mapState(['autorizacao'])
    },
    methods: {
        atualizar() {
            var url = 'anotacao';
            if(this.texto) {
                url = 'anotacao';
            }
            axios.get(encodeURI(url))
                .then(res => {
                    this.anotacoes = res.data;
                })
                .catch(error => { console.log(error) });
        },

        doCadastrar() {
            axios.post('anotacao',
                {
                    texto: this.texto,
                })
                .then(response => {
                    console.log(response);
                }).then(this.atualizar)
        }
    },
    created() {
        this.atualizar();
    }
}
</script>
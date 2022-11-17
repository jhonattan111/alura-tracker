<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        <Cronometro :tempoEmMilisegundos="tempoEmMilisegundos"/>
        <div v-if="!cronometroRodando">
            <Botao :nomeBotao="botaoPlay.nomeBotao" :iconeBotao="botaoPlay.iconeBotao" :botao-habilitado="!cronometroRodando" @click="iniciar" />
        </div>
        <div v-else>    
            <Botao :nomeBotao="botaoPause.nomeBotao" :iconeBotao="botaoPause.iconeBotao" :botao-habilitado="cronometroRodando" @click="finalizar"/>
        </div>
    </div>
</template>

<script lang="ts">
    
    import { defineComponent } from "vue";
    import Cronometro from "./Cronometro.vue";
    import Botao from "./Botao.vue";

    export default defineComponent({
        name: "Temporizador",
        emits: ['aoTemporizadorFinalizado', 'aoCronometroIniciado', 'aoCronometroFinalizado'],
        data() {
            return {    
                tempoEmMilisegundos: 0,
                cronometro: 0,
                cronometroRodando: false,
                botaoPlay: {
                    nomeBotao: "play",
                    iconeBotao: "fa-play"
                },
                botaoPause: {
                    nomeBotao: "pause",
                    iconeBotao: "fa-stop"
                }
            }
        },
        methods: {
            iniciar() {
                this.cronometroRodando = !this.cronometroRodando;
                this.cronometro = setInterval(() => {
                    this.tempoEmMilisegundos += 10;
                }, 10);
            },
            finalizar() {
                this.cronometroRodando = !this.cronometroRodando;
                clearInterval(this.cronometro);
                this.$emit('aoTemporizadorFinalizado', this.tempoEmMilisegundos);
                this.tempoEmMilisegundos = 0;
            }
        },
        components: {
            Cronometro,
            Botao,
        }
    });
</script>
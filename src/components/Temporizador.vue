<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        <Cronometro :tempoEmSegundos="tempoEmSegundos"/>
        <Botao :nomeBotao="botaoPlay.nomeBotao" :iconeBotao="botaoPlay.iconeBotao" :botao-habilitado="!cronometroRodando" @click="iniciar" />
        <Botao :nomeBotao="botaoPause.nomeBotao" :iconeBotao="botaoPause.iconeBotao" :botao-habilitado="cronometroRodando" @click="finalizar"/>
    </div>
</template>

<script lang="ts">
    
    import { defineComponent } from "vue";
    import Cronometro from "./Cronometro.vue";
    import Botao from "./Botao.vue";

    export default defineComponent({
        name: "Temporizador",
        emits: ['aoTemporizadorFinalizado'],
        data() {
            return {    
                tempoEmSegundos: 0,
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
                    this.tempoEmSegundos += 1;
                }, 1000);
            },
            finalizar() {
                this.cronometroRodando = !this.cronometroRodando;
                clearInterval(this.cronometro);
                this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos);
                this.tempoEmSegundos = 0;
            }
        },
        components: {
            Cronometro,
            Botao,
        }
    });
</script>
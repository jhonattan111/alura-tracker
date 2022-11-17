<template>
    <Box>
        <div class="columns tarefa">
            <div class="column is-7">
                {{tarefa.descricao || "Tarefa sem descrição" }}
            </div>
            <div class="column">
                <Cronometro :tempoEmMilisegundos="tarefa.duracaoEmMilisegundos"/>
            </div>
            <div class="column fa fa-trash ultima-coluna apagar-tarefa" @click="apagarTarefa"/>
        </div>
    </Box>
</template>

<script lang="ts">
    import ITarefa from '@/interfaces/ITarefa';
    import { defineComponent, PropType } from 'vue';
    import Cronometro from './Cronometro.vue';
    import Box from './Box.vue';

    export default defineComponent({
        name: 'Tarefa',
        components: {
            Cronometro,
            Box
        },
        methods: {
            apagarTarefa() {
                this.$emit("aoApagarTarefa", {
                })
            }
        },
        emits: ['aoApagarTarefa'],
        props: {
            tarefa: {
                type: Object as PropType<ITarefa>,
                required: true
            }
        }
    });
</script>

<style scoped>
    .tarefa :nth-child(2) :first-child :first-child {
        color: black;
    }

    .apagar-tarefa:hover {
        cursor: pointer;
    }
</style>
<template>
    <button class="button" :disabled="!botaoHabilitado">
        <span class="icon">
            <i class="fas" :class="[iconeBotao]"></i>
        </span>
        <span>{{nomeBotao}}</span>
    </button>
</template>

<script lang="ts">
    import { defineComponent } from 'vue';
    export default defineComponent({
        name: "Botao",
        props: {
            nomeBotao: {
                type: String,
                default: 'Botao',
            },
            botaoHabilitado: {
                type: Boolean,
                default: true,
            },
            iconeBotao: {
                type: String,
                default: 'fa-heart'
            }
        },
        methods: {
        }
    })

</script>

<template>
    <section>
        <strong class="display">{{ tempoDecorrido }}</strong>
    </section>
</template>

<script lang="ts">
    import { defineComponent } from 'vue'

    export default defineComponent ({
        name: "Cronometro",
        props: {
            tempoEmMilisegundos: {
                type: Number,
                default: 0,
            }
        },
        computed: {
            tempoDecorrido(): string {
                return new Date(this.tempoEmMilisegundos).toISOString().substring(11, 23);
            }
        },
    })
</script>

<style scoped>
 .display {
    color: var(--txt-primario)
 }

</style>
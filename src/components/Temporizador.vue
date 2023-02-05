<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        <Cronometro :tempo-em-segundos="tempoEmsegundos"/>
        <button class="button" @click="iniciar" :disabled="contrometroPlay">
            <span class="icon">
                <i class="fas fa-play"></i>
            </span> 
            <span>play</span>
        </button>
        <button class="button" @click="finalizar" :disabled="!contrometroPlay">
            <span class="icon">
                <i class="fas fa-stop"></i>
            </span> 
            <span>stop</span>
        </button>
    </div>
</template>
<script lang="ts">
import { defineComponent } from 'vue';
import Cronometro from './Cronometro.vue'
export default defineComponent ({
    name: 'Temporizador',
    emits: ['aoTemporizadorFinalizado'],
    components: {
        Cronometro
    },
    data(){
        return {
            tempoEmsegundos: 0,
            cronometro     : 0,
            contrometroPlay: false
        }
    },
    methods: {
        iniciar(){
            this.contrometroPlay = true
            this.cronometro = setInterval(() => {
                this.tempoEmsegundos += 1
            }, 1000)
        },
        finalizar(){
            this.contrometroPlay = false
            clearInterval(this.cronometro)
            this.$emit('aoTemporizadorFinalizado',this.tempoEmsegundos)
            this.tempoEmsegundos = 0
        }
    }   
});
</script>
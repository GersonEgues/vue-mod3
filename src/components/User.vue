<script setup lang="ts">
    import {ref,onMounted} from 'vue'

    let contador = 0;

    function increment() {
        contador++;
        console.log(contador);        
    }

    function getRoles(){

    }

    onMounted(()=>{
        console.log(`the initial count is ${contador}`);
        getRoles();
    });
</script>

<template>
    <div class="card">
        <h1>holaaaa</h1>

        <button type="button" 
                class="btn btn-primary"
                @click="increment">
            Incrementar
        </button>
    </div>
</template>

<style>
</style>
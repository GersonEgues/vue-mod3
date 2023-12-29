<script setup lang="ts">
    import {ref,onMounted} from 'vue'

    const count = ref(0)

    function increment(value:number) {
        count.value++;
    }

    onMounted(()=>{
        console.log(`the initial count is ${count.value}`);
    });
</script>

<template>
    <h1>holaaaa</h1>

    <button>test click</button>
</template>

<style>
</style>
<script setup lang="ts">
    import {ref,onMounted} from 'vue'
    import axios from "axios";


    let contador = 0;

    function increment() {
        contador++;
        console.log(contador);        
    }

    function getRoles(){
        axios.get('http://localhost:8083/api/rol/list')
        .then(res=>{
            console.log(res);
        })
        .catch(err=>{
            console.log(err);
        });
    }

    onMounted(()=>{
        console.log(`the initial count is ${contador}`);
        getRoles();
    });
</script>

<template>
  <div class="card">
    <label class="m-3 fw-bold">DATOS DEL USUARIO</label>
    <form class="m-3">
      <div class="mb-3">
        <label for="userName" class="form-label">User Name</label>
        <input type="text" class="form-control" id="userName">
      </div>
      
      <div class="mb-3">
        <label for="password" class="form-label">Password</label>
        <input type="password" class="form-control" id="password">
      </div>

      <div class="mb-3">
        <label for="email" class="form-label">Email</label>
        <input type="email" class="form-control " id="email">
      </div>
                
      <button type="submit" class="btn btn-primary">Submit</button>
    </form>     
  </div>
</template>

<style>
</style>
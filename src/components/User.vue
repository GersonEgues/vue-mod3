<script setup lang="ts">
    import {ref,onMounted} from 'vue'
    import axios from "axios"

    let contador = 0;
    let userRolList:any = [];

    let userRol:any = {};

    function createUser() {
      console.log("create user");
      console.log(userRol);
    }

    function cancelCreateUser() {
      console.log("cancel create user");
    }

    function getRoles(){
        axios.get('http://localhost:8083/api/rol/list')
        .then(res=>{
            userRolList = res.data;
            console.log(userRolList);
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
    <label class="m-3 fw-bold text-center">DATOS DEL USUARIO</label>
    <form class="m-3" @submit.prevent>
      <div class="mb-3">
        <label for="userName" class="form-label fw-bold">User Name</label>
        <input  type="text" 
                class="form-control" 
                id="userName"
                v-model="userRol.userName">
      </div>
      
      <div class="mb-3">
        <label for="password" class="form-label fw-bold">Password</label>
        <input  type="password" 
                class="form-control" 
                id="password"
                v-model="userRol.password">
      </div>

      <div class="mb-3">
        <label for="email" class="form-label fw-bold">Email</label>
        <input  type="email" 
                class="form-control" 
                id="email"
                v-model="userRol.email">
      </div>

      <div class="mb-3">
        <label for="firstName" class="form-label fw-bold">Primer Nombre</label>
        <input  type="text" 
                class="form-control" 
                id="firstName"
                v-model="userRol.firstName">
      </div>

      <div class="mb-3">
        <label for="lastName" class="form-label fw-bold">Segundo Nombre</label>
        <input  type="text" 
                class="form-control" 
                id="lastName"
                v-model="userRol.lastName">
      </div>

      <div class="row mb-3">
        <div class="col-6">
          <label for="age" class="form-label fw-bold">Edad</label>
          <input  type="number" 
                  class="form-control" 
                  id="age"
                  v-model="userRol.age">
        </div>

        <div class="col-6">
          <label for="birthDay" class="form-label fw-bold">Fecha de Nacimiento</label>
          <input  type="date" 
                  class="form-control" 
                  id="birthDay"
                  v-model="userRol.birthDay">  
        </div>
      </div>

      <div class="mb-3">
        <label for="rol" class="form-label fw-bold">Rol</label>
        <select class="form-select" 
                v-model="userRol.rolId">
          <option selected disabled>Seleccione un rol...</option>
          <option>A</option>
          <option>B</option>
          <option>C</option>
          <option value="rol.id" v-for="rol in userRolList">
            {{ rol.name }}
          </option>
        </select>
      </div>

      <div class="d-flex justify-content-center">
        <button class="btn btn-danger mx-1" @click="cancelCreateUser()">CANCELAR</button>
        <button class="btn btn-primary mx-1"  @click="createUser()">GUARDAR</button>
      </div>
    </form>     
  </div>
</template>

<style>
</style>
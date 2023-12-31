<script setup lang="ts">
    import {ref,onMounted} from 'vue'
    import axios from "axios"

    let contador = 0;
    let userRolList:any = [];
    let userRol:any = {};


    let userResponseList:any[];
    

    function createUser() {
      console.log("create user");
      console.log(userRol);

      let objectUserRol = {
        userName   : userRol.userName,
        password   : userRol.password,
        email      : userRol.email,
        createedAt : "2023-12-30 00:00:00",
        userDetailReq : {
          firstName : userRol.firstName, 
          lastName  : userRol.lastName, 
          age       : userRol.age, 
          birthDay  : userRol.birthDay, 
          userId    : 0, 
        },
        userRolReqList : [
          {
            userId     : 0,
            rolId      : getRolId(userRol.nameRol),
            active     : true,
            createedAt : "2023-12-30 00:00:00",
          }
        ]
      }
      
      console.log("===============");
      console.log(objectUserRol);
      console.log("===============");   
      
      createUserRest(objectUserRol);
    }

    function getRolId(name:string){
      let rolId:number=0;
      userRolList.forEach((rol:any) => {
        if(rol.name == name){
          rolId = rol.id;
        }        
      }); 
      return rolId;
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

    function createUserRest(userObject:any){
      axios.post("http://localhost:8083/api/user/data",userObject)
      .then(res=>{
        console.log(res);
        getUserResponse();
      })
      .catch(err=>{
        console.log(err);        
      });
    }

    function getUserResponse(){
        axios.get('http://localhost:8083/api/user/list')
        .then(res=>{
            userResponseList = res.data;
            console.log(userResponseList);
        })
        .catch(err=>{
            console.log(err);
        });
    }

    onMounted(()=>{
        console.log(`the initial count is ${contador}`);
        getRoles();
        getUserResponse();
    });
</script>

<template>
  <div class="card mb-2">
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
                v-model="userRol.nameRol">
          <option selected disabled>Seleccione un rol...</option>
          <option v-for="rol in userRolList">
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

  <div class="card">
    <label class="m-3 fw-bold text-center">LISTA DE USUARIOS</label>
    <div>
      <table class="table">
        <thead>
          <tr>
            <th class="fw-bold " scope="col">Nro. </th>
            <th class="fw-bold " scope="col">User Name</th>
            <th class="fw-bold " scope="col">Email</th>
          </tr>
        </thead> 
        <tbody>
          <tr v-for="(user,index) in userResponseList">
            <th scope="row">{{ index + 1 }}</th>
            <td>{{ user.username }}</td>
            <td>{{ user.email }}</td>
          </tr>
        </tbody>
    </table>
    </div>
  </div>
</template> 
<style>
</style>
<template>
  <div class="mt-5 container">
    <h1>Editar Tarea</h1>
    <div class="card">
      <div class="card-header">
        <h4>Actualiza tu  tarea 
          <NuxtLink to="/homework" class="btn btn-danger float-end">Atrás</NuxtLink>
        </h4>
      </div>
      <div class="card-body">
        <div v-if="loading">
          <loading :title="loadingText"/>
        </div>
        <div v-else>
          <form @submit.prevent="updateHomework">
            <div class="m-3">
              <label for="nombre">Nombre</label>
              <input type="text" v-model="homework.name" class="form-control" id="nombre">
            </div>
            <div class="m-3">
              <label for="description">Descripción</label>
              <textarea type="text" v-model="homework.description" class="form-control" id="description"></textarea>
            </div>
            <div class="m-3">
              <label for="fecha_limite">Fecha límite</label>
              <input type="date" v-model="homework.date" class="form-control" id="fecha_limite">
            </div>
            <div class="m-3">
              <button type="submit" class="btn btn-primary">Actualizar</button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
  export default {
      name: 'homeworkEdit',
      data() {
          return {
              homeworkId: '',
              homework:{},
              loading: false,
              loadingText: 'Cargando',                
          }
      },
          mounted() {
              this.homeworkId = this.$route.params.id;
              console.log(this.homeworkId);

              this.getHomework(this.homeworkId);
            },
      methods:{
          getHomework(homeworkId){
              axios.get(`http://127.0.0.1:8000/api/homework/${homeworkId}/`).then(res=>{
                  console.log(res)
                  this.homework = res.data.id
                  console.log(this.homework.id)
              })
          },
          updateHomework(){
              this.loading = true;
              this.loadingText = 'Guardando'

              axios.put (`http://127.0.0.1:8000/api/homework/${homeworkId}/`).then(res =>{
                  console.log(res, 'res')
                  alert("exito");

                  this.homework.name = ''
                  this.homework.description = ''
                  this.homework.date = ''
                  this.loading = false;
                  this.loadingText = 'Cargando'
              }).catch(e => {
                  console.log("error")
              });
          }
      }
  }
</script>

<style lang="scss" scoped>

</style>
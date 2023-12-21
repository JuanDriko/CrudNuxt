<template>
  <div class="container mt-5">
    <div class="card">
      <div class="card-header">
        <h4>
          Tareas
          <NuxtLink to="/homework/create" class="btn btn-primary float-end">
            Agregar tarea</NuxtLink
          >
        </h4>
      </div>
      <div class="card-body">
        <div v-if="loading">
          <loading title="Cargando..." />
        </div>
        <div v-else>
          <table class="table table-striped table-bordered">
            <thead>
              <tr>
                <th>ID</th>
                <th>Nombre</th>
                <th>Descripción</th>
                <th>Fecha</th>
                <th>Acción</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(homework, index) in homework" :key="index">
                <td>{{ homework.id }}</td>
                <td>{{ homework.name }}</td>
                <td>{{ homework.description }}</td>
                <td>{{ homework.date }}</td>
                <td>
                  <NuxtLink
                    :to="`/homework/${homework.id}`"
                    class="btn btn-success btn-sm mx-2"
                    >Editar</NuxtLink
                  >
                  <button
                    @click="deleteHomework(homework.id)"
                    type="button"
                    class="btn btn-danger btn-sm mx-2"
                  >
                    Eliminar
                  </button>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Swal from "sweetalert2";

export default {
  name: "homeworks",
  loading: true,
  data() {
    return {
      homework: {},
    };
  },
  mounted() {
    this.getHomeworks();
    console.log(this.getHomeworks());
  },
  methods: {
    getHomeworks() {
      axios.get(`http://127.0.0.1:8000/api/homework/`).then((res) => {
        this.homework = res.data;
      });
    },
    deleteHomework(homeworkId) {
      Swal.fire({
        title: "¿Estás seguro?",
        text: "Esta acción eliminará el elemento. ¿Estás seguro de continuar?",
        icon: "warning",
        showCancelButton: true,
        confirmButtonColor: "#3085d6",
        cancelButtonColor: "#d33",
        confirmButtonText: "Sí, eliminarlo",
      }).then((result) => {
        if (result.isConfirmed) {
          axios
            .delete(`http://127.0.0.1:8000/api/homework/${homeworkId}/`)
            .then((res) => {
              Swal.fire(
                "¡Eliminado!",
                "El elemento ha sido eliminado correctamente.",
                "success"
              );
              this.getHomeworks();
            })
            .catch((error) => {
              Swal.fire(
                "Error",
                "Hubo un problema al intentar eliminar el elemento.",
                "error"
              );
            });
        }
      });
    },
  },
};
</script>

<style lang="scss" scoped></style>


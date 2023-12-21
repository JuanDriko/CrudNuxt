<template>
  <div class="mt-5 container">
    <h1>Crear Tarea</h1>
    <div class="card">
      <div class="card-header">
        <h4>
          Agregar tarea
          <NuxtLink to="/homework" class="btn btn-danger float-end"
            >Atrás</NuxtLink
          >
        </h4>
      </div>
      <div class="card-body">
        <div v-if="loading">
          <loading :title="loadingText" />
        </div>
        <div v-else>
          <form @submit.prevent="saveHomework">
            <div class="m-3">
              <label for="nombre">Nombre</label>
              <input
                type="text"
                v-model="homework.name"
                class="form-control"
                id="nombre"
              />
            </div>
            <div class="m-3">
              <label for="description">Descripción</label>
              <textarea
                type="text"
                v-model="homework.description"
                class="form-control"
                id="description"
              ></textarea>
            </div>
            <div class="m-3">
              <label for="fecha_limite">Fecha límite</label>
              <input
                type="date"
                v-model="homework.date"
                class="form-control"
                id="fecha_limite"
              />
            </div>
            <div class="m-3">
              <button type="submit" class="btn btn-primary">Guardar</button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Swal from "sweetalert2";

export default {
  name: "homeworkCreate",
  data() {
    return {
      homework: {
        name: "",
        description: "",
        date: "",
      },
      loading: false,
      loadingText: "Cargando",
    };
  },
  methods: {
    saveHomework() {
      this.loading = true;
      this.loadingText = "Guardando";

      axios
        .post(`http://127.0.0.1:8000/api/homework/`, this.homework)
        .then((res) => {
          console.log(res, "res");
          Swal.fire(
            "Guardado",
            "El elemento ha sido guardado correctamente.",
            "success"
          );
          this.homework.name = "";
          this.homework.description = "";
          this.homework.date = "";
          this.loading = false;
          this.loadingText = "Cargando";
        })
        .catch((e) => {
          Swal.fire(
            "Error",
            "Hubo un problema al intentar guardar el elemento.",
            "error"
          );
          console.log("error");
        });
    },
  },
};
</script>

<style lang="scss" scoped></style>
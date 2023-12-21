<template>
    <div>
        <nav class="navbar navbar-expand-lg bg-body-tertiary">
  <div class="container">
    <NuxtLink to="/" class="navbar-brand" >AppHomework</NuxtLink>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
        <li class="nav-item">
          <NuxtLink class="nav-link active" aria-current="page" to="/">Inicio</NuxtLink>
        </li>
        <li class="nav-item">
          <NuxtLink class="nav-link" to="/homework">Tareas</NuxtLink>
        </li>
        <li class="nav-item">
          <NuxtLink class="nav-link" to="/contact">Contacto</NuxtLink>
        </li>
        <li class="nav-item">
          <NuxtLink class="nav-link" to="/about">Acerca de</NuxtLink>
        </li>
      </ul>
    </div>
  </div>
</nav>
    </div>
</template>

<script setup>
</script>

<style lang="scss" scoped>

</style>
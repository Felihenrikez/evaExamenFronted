<template>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Mi Aplicación</a>
        <ul class="navbar-nav">
          <li class="nav-item">
            <a class="nav-link" @click="selectTab('calculator')">Cálculo de Calificaciones</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" @click="selectTab('registration')">Formulario de Registro</a>
          </li>
        </ul>
      </div>
    </nav>
  </template>
  
  <script>
  export default {
    methods: {
      selectTab(tab) {
        this.$emit('change-tab', tab);
      },
    },
  };
  </script>
  
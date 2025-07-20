<script setup>
  import { 
    BNavbar, 
    BNavbarBrand, 
    BNavbarToggle, 
    BCollapse, 
    BNavbarNav, 
    BNavItem,
    BNavForm, 
    BFormInput, 
    BButton 
  } from 'bootstrap-vue-next'
</script>

<template>
  <div>
    <BNavbar toggleable="lg" variant="light" class="border-bottom px-3">
      <BNavbarBrand href="#">Programación Front End</BNavbarBrand>
      
      <BNavbarToggle target="nav-collapse" />

      <BCollapse id="nav-collapse" is-nav>
        <BNavbarNav>
          <router-link to="/" class="nav-link">Cálculo de calificaciones</router-link>
          <router-link to="/registro" class="nav-link">Formulario de Registro</router-link>
          <BNavItem href="#" disabled>En construcción</BNavItem>
        </BNavbarNav>
        
        <BNavbarNav class="ms-auto mb-2 mb-lg-0">
          <BNavForm @submit.prevent>
            <BFormInput
              class="me-2"
              placeholder="Search"
            />
            <BButton variant="outline-success" type="submit">Búsqueda</BButton>
          </BNavForm>
        </BNavbarNav>
      </BCollapse>
    </BNavbar>

    <main class="container my-5">
      <router-view />
    </main>
  </div>
</template>

<style>
  .router-link-exact-active {
    font-weight: bold;
    color: #1a8754 !important;
  }

  .navbar-brand {
    color: rgba(0, 0, 0, 0.9) !important;
  }
</style>
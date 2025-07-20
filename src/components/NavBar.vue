<template>
  <BNavbar toggleable="lg" variant="light" class="border-bottom px-3">
    <BNavbarBrand href="#">Programación Front End</BNavbarBrand>
    
    <BNavbarToggle target="nav-collapse" />

    <BCollapse id="nav-collapse" v-model="navCollapseState" is-nav>
      <BNavbarNav @click="navCollapseState = false"> 
        <BNavItem to="/" active-class="text-success fw-bold">Cálculo de calificaciones</BNavItem>
        <BNavItem to="/registro" active-class="text-success fw-bold">Formulario de Registro</BNavItem>
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
</template>

<script>
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

  export default {
    name: 'AppNavbar',
    components: {
      BNavbar, 
      BNavbarBrand, 
      BNavbarToggle, 
      BCollapse, 
      BNavbarNav, 
      BNavItem,
      BNavForm, 
      BFormInput, 
      BButton
    },
    data() {
      return {
        navCollapseState: false 
      }
    }
  }
</script>

<style scoped>
  .navbar-toggler {
    border: 1px solid rgba(0, 0, 0, 0.1);
    border-radius: 6px;
    padding: 6px 8px;
    transition: all 0.2s ease;
    background-color: transparent;
  }

  .navbar-toggler:hover {
    background-color: rgba(0, 0, 0, 0.05);
    border-color: rgba(0, 0, 0, 0.15);
  }

  .navbar-toggler:focus {
    box-shadow: 0 0 0 2px rgba(46, 46, 46, 0.25);
    outline: none;
  }

  .navbar-toggler:active {
    box-shadow: 0 0 0 2px rgba(46, 46, 46, 0.25);
    transform: scale(0.98);
  }
</style>
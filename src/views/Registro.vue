<template>
  <BContainer>
    <BRow class="justify-content-center">
      <BCol md="8" lg="6">
        <BForm @submit.prevent="submitForm" novalidate>

          <BFormGroup label="Nombre:" label-for="name" class="mb-3">
            <BFormInput
              id="name"
              v-model.trim="form.name"
              type="text"
              @input="errors.name = ''" />
            <BFormInvalidFeedback :state="!errors.name">
              {{ errors.name }}
            </BFormInvalidFeedback>
          </BFormGroup>

          <BFormGroup label="Correo:" label-for="email" class="mb-3">
            <BFormInput
              id="email"
              v-model.trim="form.email"
              type="email"
              @input="errors.email = ''" />
            <BFormInvalidFeedback :state="!errors.email">
              {{ errors.email }}
            </BFormInvalidFeedback>
          </BFormGroup>

          <BFormGroup label="Contraseña:" label-for="password" class="mb-3">
            <BFormInput
              id="password"
              v-model="form.password"
              type="password"
              @input="errors.password = ''; errors.confirmPassword = ''" />
            <BFormInvalidFeedback :state="!errors.password">
              {{ errors.password }}
            </BFormInvalidFeedback>
          </BFormGroup>

          <BFormGroup label="Repetir Contraseña:" label-for="confirmPassword" class="mb-3">
            <BFormInput
              id="confirmPassword"
              v-model="form.confirmPassword"
              type="password"
              @input="errors.confirmPassword = ''" />
            <BFormInvalidFeedback :state="!errors.confirmPassword">
              {{ errors.confirmPassword }}
            </BFormInvalidFeedback>
          </BFormGroup>

          <div class="d-flex justify-content-start">
            <BButton type="submit" variant="success" class="btn-w">
              Enviar
            </BButton>
          </div>
        </BForm>
      </BCol>
    </BRow>
  </BContainer>
</template>

<script>
  import { 
    BContainer, 
    BRow, 
    BCol, 
    BForm, 
    BFormGroup, 
    BFormInput, 
    BButton, 
    BFormInvalidFeedback 
  } from 'bootstrap-vue-next';

  export default {
    name: "RegistrationFormBootstrap",
    components: {
      BContainer,
      BRow,
      BCol,
      BForm,
      BFormGroup,
      BFormInput,
      BButton,
      BFormInvalidFeedback
    },
    data() {
      return {
        form: {
          name: "",
          email: "",
          password: "",
          confirmPassword: "",
        },
        errors: {},
      };
    },
    computed: {
      passwordsDoNotMatch() {
        if (this.form.password && this.form.confirmPassword) {
          return this.form.password !== this.form.confirmPassword;
        }
        return false;
      }
    },
    methods: { 
      validateForm() {
        this.errors = {};
        
        if (!this.form.name) {
          this.errors.name = "El campo nombre es requerido";
        } else if (/\d/.test(this.form.name)) {
          this.errors.name = "El nombre no puede contener números";
        }

        const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        if (!this.form.email) {
          this.errors.email = "El campo correo es requerido";
        } else if (!emailRegex.test(this.form.email)) {
          this.errors.email = "El formato del correo no es válido";
        }

        if (!this.form.password) {
          this.errors.password = "El campo contraseña es requerido";
        }

        if (!this.form.confirmPassword) {
          this.errors.confirmPassword = "El campo repetir contraseña es requerido";
        } else if (this.passwordsDoNotMatch) {
          this.errors.confirmPassword = "Las contraseñas no coinciden";
        }

        return Object.keys(this.errors).length === 0;
      },

      submitForm() {
        if (this.validateForm()) {
          alert("El registro se ha realizado correctamente");
          this.form = { name: '', email: '', password: '', confirmPassword: '' };
          this.errors = {};
        }
      },
    },
  };
</script>

<style scoped>
  .btn-w {
    width: 100px;
  }
</style>
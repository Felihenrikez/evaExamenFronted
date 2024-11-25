<template>
  <div>
    <h2>Formulario de Registro</h2>
    <form @submit.prevent="validateForm">
      <div class="mb-3">
        <label for="name" class="form-label">Nombre:</label>
        <input
          type="text"
          v-model="form.name"
          class="form-control"
          id="name"
          @blur="validateField('name')"
          :class="{ 'is-invalid': errors.name }"
          required
        />
        <div v-if="errors.name" class="invalid-feedback">
          {{ errors.name }}
        </div>
      </div>
      <div class="mb-3">
        <label for="email" class="form-label">Correo:</label>
        <input
          type="email"
          v-model="form.email"
          class="form-control"
          id="email"
          @blur="validateField('email')"
          :class="{ 'is-invalid': errors.email }"
          required
        />
        <div v-if="errors.email" class="invalid-feedback">
          {{ errors.email }}
        </div>
      </div>
      <div class="mb-3">
        <label for="password" class="form-label">Contraseña:</label>
        <input
          type="password"
          v-model="form.password"
          class="form-control"
          id="password"
          @blur="validateField('password')"
          :class="{ 'is-invalid': errors.password }"
          required
        />
        <div v-if="errors.password" class="invalid-feedback">
          {{ errors.password }}
        </div>
      </div>
      <div class="mb-3">
        <label for="confirmPassword" class="form-label">Repetir Contraseña:</label>
        <input
          type="password"
          v-model="form.confirmPassword"
          class="form-control"
          id="confirmPassword"
          @blur="validateField('confirmPassword')"
          :class="{ 'is-invalid': errors.confirmPassword }"
          required
        />
        <div v-if="errors.confirmPassword" class="invalid-feedback">
          {{ errors.confirmPassword }}
        </div>
      </div>
      <button type="submit" class="btn btn-success">Enviar</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        name: "",
        email: "",
        password: "",
        confirmPassword: "",
      },
      errors: {
        name: null,
        email: null,
        password: null,
        confirmPassword: null,
      },
    };
  },
  methods: {
    validateField(field) {
      const value = this.form[field];
      switch (field) {
        case "name":
          this.errors.name = value.trim()
            ? null
            : "El campo nombre es obligatorio.";
          break;
        case "email":
          const emailRegex =
            /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
          this.errors.email = emailRegex.test(value)
            ? null
            : "El correo no tiene un formato válido.";
          break;
        case "password":
          this.errors.password = value.trim().length >= 6
            ? null
            : "La contraseña debe tener al menos 6 caracteres.";
          break;
        case "confirmPassword":
          this.errors.confirmPassword =
            value === this.form.password
              ? null
              : "Las contraseñas no coinciden.";
          break;
        default:
          break;
      }
    },
    validateForm() {
      // Validar todos los campos
      Object.keys(this.form).forEach((field) => {
        this.validateField(field);
      });

      // Verificar si hay errores
      const hasErrors = Object.values(this.errors).some(
        (error) => error !== null
      );

      if (!hasErrors) {
        alert("El registro se ha realizado correctamente.");
        this.resetForm();
      } else {
        alert("Por favor, corrige los errores antes de continuar.");
      }
    },
    resetForm() {
      this.form = {
        name: "",
        email: "",
        password: "",
        confirmPassword: "",
      };
      this.errors = {
        name: null,
        email: null,
        password: null,
        confirmPassword: null,
      };
    },
  },
};
</script>

<style>

</style>

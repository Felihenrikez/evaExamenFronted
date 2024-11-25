<template>
  <div>
    <h2>Cálculo de Calificaciones</h2>
    <form @submit.prevent="calculate">
      <div class="mb-3" v-for="(label, key) in gradeLabels" :key="key">
        <label :for="key" class="form-label">{{ label }}</label>
        <input
          type="number"
          v-model.number="grades[key]"
          class="form-control"
          :id="key"
          @blur="validateGrade(key)"
          :class="{ 'is-invalid': errors[key] }"
          required
        />
        <div v-if="errors[key]" class="invalid-feedback">
          {{ errors[key] }}
        </div>
      </div>
      <div class="mb-3">
        <label for="attendance" class="form-label">Asistencia (%):</label>
        <input
          type="number"
          v-model.number="attendance"
          class="form-control"
          id="attendance"
          min="0"
          max="100"
          required
        />
      </div>
      <button type="submit" class="btn btn-primary">Calcular</button>
    </form>
    <div v-if="result !== null" class="mt-4">
      <p>Promedio Ponderado: {{ result.average }}</p>
      <p>{{ result.message }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      grades: { grade1: null, grade2: null, grade3: null },
      attendance: null,
      result: null,
      errors: { grade1: null, grade2: null, grade3: null },
      gradeLabels: {
        grade1: "Nota 1 (35%):",
        grade2: "Nota 2 (35%):",
        grade3: "Nota 3 (30%):",
      },
    };
  },
  methods: {
    validateGrade(key) {
      const value = this.grades[key];
      if (value < 10) {
        this.errors[key] = "El valor debe ser superior a 10";
      } else if (value > 70) {
        this.errors[key] = "El valor debe ser inferior o igual a 70";
      } else {
        this.errors[key] = null;
      }
    },
    calculate() {
      // Validar que no haya errores antes de proceder
      Object.keys(this.grades).forEach((key) => this.validateGrade(key));
      if (Object.values(this.errors).some((error) => error !== null)) {
        alert("Corrige los errores antes de calcular");
        return;
      }

      const { grade1, grade2, grade3 } = this.grades;
      // Calcular el promedio ponderado con los porcentajes 
      const average = (
        grade1 * 0.35 +
        grade2 * 0.35 +
        grade3 * 0.3
      ).toFixed(2);

      // Evaluar aprobacion
      const message =
        average >= 40 && this.attendance >= 80
          ? "Aprobado"
          : "Reprobado";
      this.result = { average, message };
    },
  },
};
</script>

<style>
/* Opcional: personalizar estilos */
</style>

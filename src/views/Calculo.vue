<template>
  <div class="row justify-content-center">
    <div class="col-md-6 col-lg-5">
      <form @submit.prevent="handleSubmit" ref="formRef" novalidate>
        <BFormGroup label="Nota 1" label-for="grade1" class="mb-3 text-center">
          <BFormInput
            id="grade1"
            v-model.number="form.grade1"
            type="number"
            placeholder="Nota 1"
            required
            min="10"
            max="70"
            @input="clearCustomValidity"
            @invalid="handleInvalidGrade"
          />
        </BFormGroup>

        <BFormGroup label="Nota 2" label-for="grade2" class="mb-3 text-center">
          <BFormInput
            id="grade2"
            v-model.number="form.grade2"
            type="number"
            placeholder="Nota 2"
            required
            min="10"
            max="70"
            @input="clearCustomValidity"
            @invalid="handleInvalidGrade"
          />
        </BFormGroup>

        <BFormGroup label="Nota 3" label-for="grade3" class="mb-3 text-center">
          <BFormInput
            id="grade3"
            v-model.number="form.grade3"
            type="number"
            placeholder="Nota 3"
            required
            min="10"
            max="70"
            @input="clearCustomValidity"
            @invalid="handleInvalidGrade"
          />
        </BFormGroup>

        <BFormGroup label="Asistencia %" label-for="attendance" class="mb-3 text-center">
          <BFormInput
            id="attendance"
            v-model.number="form.attendance"
            type="number"
            placeholder="Asistencia"
            required
            min="0"
            max="100"
            @input="clearCustomValidity"
            @invalid="handleInvalidAttendance"
          />
        </BFormGroup>

        <div class="d-grid">
          <BButton type="submit" variant="primary">Calcular</BButton>
        </div>
      </form>

      <div v-if="showGeneralError" class="text-danger text-center mt-3">
        Por favor, ingrese valores válidos para las notas y la asistencia
      </div>

      <div v-if="result.average !== null" class="mt-4 text-center">
        <h3>El promedio es: {{ result.average.toFixed(2) }}</h3>
        <h3 :class="result.status === 'Aprobado' ? 'text-success' : 'text-danger'">
          Tu estado es: {{ result.status }}
        </h3>
      </div>
    </div>
  </div>
</template>

<script>
  import { BFormGroup, BFormInput, BButton } from 'bootstrap-vue-next';

  export default {
    name: 'GradesForm',
    components: {
      BFormGroup,
      BFormInput,
      BButton,
    },
    data() {
      return {
        form: {
          grade1: null,
          grade2: null,
          grade3: null,
          attendance: null,
        },
        result: {
          average: null,
          status: '',
        },
        showGeneralError: false,
      };
    },
    methods: {
      handleSubmit() {
        this.result.average = null;
        this.result.status = '';
        const form = this.$refs.formRef;

        if (!form.checkValidity()) {
          this.showGeneralError = true;
          form.reportValidity();
          return;
        }

        this.showGeneralError = false;

        const average =
          this.form.grade1 * 0.35 +
          this.form.grade2 * 0.35 +
          this.form.grade3 * 0.30;

        this.result.average = average;
        this.result.status =
          average >= 40 && this.form.attendance >= 80
            ? 'Aprobado'
            : 'Reprobado';
      },

      clearCustomValidity(event) {
        event.target.setCustomValidity('');
        this.showGeneralError = false;
        this.result.average = null;
      },

      handleInvalidGrade(event) {
        const validity = event.target.validity;
        if (validity.rangeUnderflow) {
          event.target.setCustomValidity('El valor debe ser superior o igual a 10');
        } else if (validity.rangeOverflow) {
          event.target.setCustomValidity('El valor debe ser inferior o igual a 70');
        } else if (validity.valueMissing) {
          event.target.setCustomValidity('Este campo es obligatorio');
        }
      },
      
      handleInvalidAttendance(event) {
        const validity = event.target.validity;
        if (validity.rangeUnderflow) {
          event.target.setCustomValidity('El valor debe ser superior o igual a 0');
        } else if (validity.rangeOverflow) {
          event.target.setCustomValidity('El valor debe ser inferior o igual a 100');
        } else if (validity.valueMissing) {
          event.target.setCustomValidity('Este campo es obligatorio');
        }
      },
    },
  };
</script>
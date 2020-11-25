<template>
  <div class="m-3">
    <b-card>
      <div class="title">RESERVAR</div>
      <p v-if="errors" class="row justify-content-center" style="color: red">
        {{ errors }}
      </p>
      <b-form
        @submit.prevent="create"
        @reset.prevent="onReset"
        inline
        v-if="show"
      >
        <div>
          <label for="name">Nombre</label>
          <b-form-input
            id="name"
            v-model="form.name"
            placeholder="Ingresar nombre"
          ></b-form-input>
        </div>
        <div>
          <label for="date">Fecha</label>
          <b-form-datepicker
            id="date"
            v-model="form.date"
            placeholder="Seleccionar"
            size="sm"
          ></b-form-datepicker>
        </div>
        <div>
          <label for="startTime">Desde</label>
          <b-form-timepicker
            id="startTime"
            v-model="form.startTime"
            locale="en"
            placeholder="Hora inicio"
            size="sm"
          ></b-form-timepicker>
        </div>
        <div>
          <label for="endTime">Hasta</label>
          <b-form-timepicker
            id="endTime"
            v-model="form.endTime"
            locale="en"
            placeholder="Hora fin"
            size="sm"
          ></b-form-timepicker>
        </div>
        <div>
          <b-button variant="success" type="submit">Guardar</b-button>
        </div>
      </b-form>
    </b-card>
  </div>
</template>

<script>
export default {
  name: "Form",
  data() {
    return {
      show: true,
      errors: "",
      form: {
        name: "",
        date: "",
        startTime: "",
        endTime: "",
      },
    };
  },
  methods: {
    create() {
      if (
        !this.form.name ||
        !this.form.date ||
        !this.form.startTime ||
        !this.form.endTime
      ) {
        this.errors = "Debe completar todos los campos para guardar la reserva";
      } else {
        const reserva = {
          content: this.form.name,
          start: `${this.form.date} ${this.form.startTime}`,
          end: `${this.form.date} ${this.form.endTime}`,
          startTime: this.form.startTime,
          endTime: this.form.endTime,
        };
        this.$emit("submit", reserva);
        this.form = {};
        this.errors = "";
      }
    },
  },
};
</script>
<style>
.title {
  font-size: 18px;
  font-weight: bold;
  color: #22ab49;
}
</style>
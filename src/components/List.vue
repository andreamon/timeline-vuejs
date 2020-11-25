<template>
  <div class="mt-5">
    <b-card>
      <template #header>
        <div class="title">Listado de reservas</div>
      </template>

      <b-row class="custom-header">
        <b-col>Nombre </b-col>
        <b-col>Horario </b-col>
        <b-col>Acción </b-col>
      </b-row>
      <div class="row" v-for="(reserva, index) in reservas" :key="index">
        <div class="col">{{ reserva.content }}</div>
        <div class="col">
          de {{ reserva.startTime }} a {{ reserva.endTime }}
        </div>
        <div class="col"><b-button variant="link" v-on:click="$emit('delete', index)" style="color:red" title="Eliminar"><i class="fas fa-trash-alt"></i></b-button></div>
      </div>
    </b-card>
  </div>
</template>
<script>
export default {
  name: "List",
  props: ["reservas"],
};
</script>
<style>
.title {
  font-size: 18px;
  font-weight: bold;
  color: #22ab49;
}
.custom-header{
  font-weight: bold;
}
</style>
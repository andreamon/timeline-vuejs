<template>
  <div>
    <Form v-on:submit="add($event)" />
    <Timeline :reservas="reservas"></Timeline>
    <List :reservas="reservas" v-on:delete="deleted($event)" />
  </div>
</template>

<script>
import Timeline from "./Timeline";
import Form from "./Form";
import List from "./List";
import Swal from "sweetalert2";

export default {
  components: { Timeline, Form, List },
  name: "Home",
  data: function () {
    return {
      reservas: [],
    };
  },
  methods: {
    add: function (reserva) {
      reserva.id = Math.random();
      this.reservas.push(reserva);
      console.log("reserva", this.reservas);
    },
    deleted: function (index) {
      Swal.fire({
        title: "Seguro que desea eliminar la reserva?",
        text: "Esta acción no podrá deshacerse",
        icon: "warning",
        showCancelButton: true,
        confirmButtonColor: "#3085d6",
        cancelButtonColor: "#d33",
        cancelButtonText: 'Cancelar',
        confirmButtonText: "Sí, eliminar!",
      }).then((result) => {
        if (result.isConfirmed) {
          this.reservas.splice(index, 1);
          Swal.fire("Eliminado", "La reserva ha sido eliminada", "success");
        }
      });
      console.log(index);
    },
  },
};
</script>

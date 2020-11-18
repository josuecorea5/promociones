<template>
  <div class="card">
    <div>
      <slot></slot>
      <div class="body-card">
        <p class="font-weight-bold">Reservaciones disponibles</p>
        <p>{{ numberReservation }}</p>
        <p>$100</p>
        <button
          id="btn-reserva"
          @click="modal"
          type="button"
          class="btn btn-primary mt-2"
          data-toggle="button"
          aria-pressed="false"
          autocomplete="off"
        >
          Reservar
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "PxPromociones",
  data() {
    return {
      numberReservation: 2,
    };
  },
  methods: {
    modal() {
      let botton = document.getElementById("btn-reserva");
      this.$swal({
        title: "Desa adquirir la promocion",
        type: "warning",
        confirmButtonText: "Solicitar!",
        showCloseButton: true,
      }).then((result) => {
        if (result.value) {
          this.$swal(
            "Gracias!",
            "La solitud se ha enviado con exito",
            "success"
          );
          this.numberReservation = this.numberReservation -= 1;
          if (this.numberReservation < 0) {
            this.$swal("Reservaciones Agotadas");
            this.numberReservation = 0;
            botton.disabled = true;
          }
        } else {
          this.$swal("Reservacion candelada");
        }
      });
    },
  },
};
</script>

<style scoped>
.card {
  width: 300px;
  height: 460px;
  border-radius: 8px;
  margin: 10px;
  box-shadow: 5px 10px 8px #888888;
  overflow: hidden;
}

.body-card {
  padding: 5px;
  text-align: center;
}
span {
  display: block;
}
p {
  margin: 0;
}
</style>

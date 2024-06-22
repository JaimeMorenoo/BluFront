<template>
  <div class="card">
    <img src="@/assets/mono.jpg" alt="" class="giveaway-image" />
    <div class="countdown">
      <div>
        <h2>0</h2>
        <p>Entradas Totales</p>
      </div>
      <div>
        <h2>1</h2>
        <p>Días Restantes</p>
      </div>
    </div>
    <div class="content">
      <h2>¡Gana una Reserva de Mesa en Nuestra Discoteca!</h2>
      <p>¡Celebra a lo grande con tus amigos ganando una reserva de mesa para 5 personas!</p>
      <div class="form-group">
        <label for="tickets">Número de Entradas:</label>
        <input type="number" :value="tickets" @input="$emit('update:tickets', +$event.target.value)" min="1" />
      </div>
      <p>Precio total: €{{ totalPrice }}</p>
      <button @click="$emit('buy-tickets')">Comprar Entradas</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    tickets: {
      type: Number,
      required: true
    },
    ticketPrice: {
      type: Number,
      required: true
    }
  },
  computed: {
    totalPrice() {
      return this.tickets * this.ticketPrice;
    }
  }
};
</script>

<style scoped>
.card {
  background: rgba(0, 0, 0, 0.6);
  border-radius: 10px;
  padding: 20px;
  margin: 0 auto;
  max-width: 350px;
  text-align: center;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  margin-bottom: 20px;
}

.giveaway-image {
  max-height: 200px;
  object-fit: cover;
  margin-bottom: 20px;
  width: 100%;
  border-radius: 10px;
}

.countdown {
  display: flex;
  justify-content: space-around;
  margin: 20px 0;
}

.countdown div {
  text-align: center;
}

.form-group {
  margin: 20px 0;
  text-align: center;
}

label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}

input[type="number"] {
  width: 40%;
  padding: 10px;
  box-sizing: border-box;
  border: 1px solid #ccc;
  border-radius: 5px;
  text-align: center;
}

button {
  background-color: #4caf50;
  color: white;
  border: none;
  padding: 10px 10px;
  font-size: 1em;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  margin-top: 20px;
}

button:hover {
  background-color: #45a049;
}
</style>

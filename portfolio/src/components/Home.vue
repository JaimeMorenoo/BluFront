<template>
  <div class="back">
    <div class="container">
      <header>
        <img src="@/assets/logo.png" alt="Logo" class="logo" />
        <h1>¡Celebra con Nosotros!</h1>
        <p>Aprovecha esta oportunidad única</p>
      </header>
      <div class="card">
        <img src="@/assets/mono.jpg" alt="" class="giveaway-image" />
        <div class="countdown">
          <div>
            <h2>0</h2>
            <p>Tus Entradas</p>
          </div>
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
          <h2>Gana una Reserva de Mesa en Nuestra Discoteca</h2>
          <p>¡Celebra a lo grande con tus amigos ganando una reserva de mesa para 5 personas!</p>
          <div class="form-group">
            <label for="tickets">Número de Entradas:</label>
            <input type="number" v-model="tickets" min="1" />
          </div>
          <button @click="buyTickets">Comprar Entradas</button>
        </div>
      </div>
      <footer>
        <p>Contáctanos</p>
        <div class="social-icons">
          <i class="fa fa-facebook"></i>
          <i class="fa fa-twitter"></i>
          <i class="fa fa-instagram"></i>
          <i class="fa fa-linkedin"></i>
        </div>
      </footer>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tickets: 1
    };
  },
  methods: {
    buyTickets() {
      alert(`Has comprado ${this.tickets} entradas`);
      // Aquí iría la lógica para procesar el pago
    }
  }
};
</script>

<style scoped>
@import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css');

.back {
  text-align: center;
  background: url('@/assets/background.jpeg') no-repeat center center fixed;
  background-size: cover;
  color: white;
  padding: 20px;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  overflow: hidden;
}

.container {
  text-align: center;
  color: white;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

header {
  margin-top: 5px;
  position: relative;
}

.logo {
  width: 300px; /* Cambia el tamaño del logo aquí */
  position: absolute;
  top: -100px;
  left: 50%;
  transform: translateX(-50%);
}

.card {
  background: rgba(0, 0, 0, 0.6);
  border-radius: 10px;
  padding:5px;
  margin: 0 auto;
  max-width: 325px;
  text-align: center;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
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

h1 {
  font-size: 2em;
  margin-top: 100px; /* Ajusta el margen superior para dar espacio al logo */
  margin-bottom: 10px;
}

h2 {
  font-size: 1.2em;
  margin: 10px 0;
}

p {
  font-size: 1em;
  margin: 10px 0;
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
  width: 100%;
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
  padding: 10px 20px;
  font-size: 1em;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #45a049;
}

footer {
  margin-top: 5px;
}

.social-icons {
  display: flex;
  justify-content: center;
  margin: 10px 0;
}

.social-icons i {
  font-size: 1.5em;
  margin: 0 10px;
  cursor: pointer;
  transition: color 0.3s ease;
}

.social-icons i:hover {
  color: #ccc;
}
</style>

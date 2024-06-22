<template>
  <div v-if="show" class="modal">
    <div class="modal-content">
      <span class="close" @click="close">&times;</span>
      <h2>Introduce tus datos</h2>
      <div class="form-group">
        <label for="email">Correo Electrónico:</label>
        <input type="text" v-model="customer.email" />
      </div>
      <div class="form-group">
        <label for="phone">Instagram:</label>
        <input type="text" v-model="customer.instagram" />
      </div>
      <button @click="submitCustomerData">Enviar</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    show: {
      type: Boolean,
      required: true
    },
    customer: {
      type: Object,
      required: true
    }
  },
  methods: {
    close() {
      this.$emit('close');
    },
    submitCustomerData() {
      // Validación básica
      if (!this.customer.email || !this.customer.instagram) {
        alert('Por favor, complete todos los campos.');
        return;
      }

      // Emitir evento para enviar datos al componente padre
      this.$emit('submit', this.customer);
    }
  }
};
</script>

<style scoped>
.modal {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgba(0,0,0,0.5);
}

.modal-content {
  background-color: #fefefe;
  margin: auto;
  padding: 20px;
  border: 1px solid #888;
  width: 80%;
  max-width: 500px;
  text-align: left;
  color: black;
  border-radius: 10px;
}

.close {
  color: #aaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close:hover,
.close:focus {
  color: black;
  text-decoration: none;
  cursor: pointer;
}

.form-group {
  margin-bottom: 15px;
}

label {
  display: block;
  font-weight: bold;
  margin-bottom: 5px;
}

input {
  width: 100%;
  padding: 10px;
  box-sizing: border-box;
  border: 1px solid #ccc;
  border-radius: 5px;
}
</style>

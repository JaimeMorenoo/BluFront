<template>
  <div class="back">
    <div class="container">
      <header>
        <img src="@/assets/logo.png" alt="Logo" class="logo" />
        <h1>¡Celebra con Nosotros!</h1>
        <p>Aprovecha esta oportunidad única</p>
      </header>
      <!-- CardComponent with event listeners -->
      <CardComponent
        :tickets="tickets"
        :ticketPrice="ticketPrice"
        @update:tickets="tickets = $event"
        @buy-tickets="showModal = true"
      />
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

    <!-- Modal form for customer data -->
    <CustomerDataForm
      :show="showModal"
      :customer="customer"
      @close="showModal = false"
      @submit="submitCustomerData"
    />
  </div>
</template>

<script>
import axios from 'axios';
import CardComponent from '@/components/CardComponent.vue';
import CustomerDataForm from '@/components/CustomerDataForm.vue';

export default {
  components: {
    CardComponent,
    CustomerDataForm
  },
  data() {
    return {
      tickets: 1,
      ticketPrice: 5,
      showModal: false,
      customer: {
        email: '',
        instagram: ''
      },
      emailExists: false  // Flag to track if email already exists
    };
  },
  methods: {
    submitCustomerData(customerData) {
      // Validate customer data
      if (!customerData.email || !customerData.instagram) {
        alert('Por favor, complete todos los campos.');
        return;
      }

      // Check if email already exists
      this.checkEmailExists(customerData.email)
        .then(exists => {
          if (exists) {
            alert('Este correo electrónico ya está registrado. Por favor, use otro.');
          } else {
            // Proceed with creating customer
            this.createCustomer(customerData);
          }
        })
        .catch(error => {
          console.error('Error checking email:', error);
          alert('Hubo un problema al verificar el correo electrónico. Por favor, inténtelo de nuevo.');
        });
    },
    checkEmailExists(email) {
      // Make GET request to check if email exists
      return axios.get(`http://192.168.4.176:5033/Customer/check-email?email=${encodeURIComponent(email)}`)
        .then(response => {
          return response.data.exists;
        })
        .catch(error => {
          console.error('Error checking email existence:', error);
          throw error;
        });
    },
    createCustomer(customerData) {
      // Make POST request to create customer using Axios
      axios.post('http://192.168.4.176:5033/Customer/create', {
        email: customerData.email,
        instagram: customerData.instagram
      })
      .then(response => {
        // Handle response data, such as setting customer ID, etc.
        console.log('Response from server (Create Customer):', response.data);

        // Example: Assume the response contains customer ID
        const customerId = response.data.customer_id; // Adjust based on your API response structure

        // Proceed to create tickets for the customer
        this.createTickets(customerId);
      })
      .catch(error => {
        console.error('Error creating customer:', error);
        alert('Hubo un problema al crear el cliente. Por favor, inténtelo de nuevo.');
      });

      // Optionally, close modal or handle UI state
      this.showModal = false;
    },
    createTickets(customerId) {
      // Make POST request to create tickets for the customer
      axios.post('http://192.168.4.176:5033/Tickets', {
        customer_id: customerId,
        event_id: 1,  // Replace with actual event ID
        venue_id: 1,  // Replace with actual venue ID
        issued_date: new Date().toISOString(),
        due_date: '2024-07-01',  // Replace with actual due date
        price: this.ticketPrice,
        qty: this.tickets,
        discount: 0
      })
      .then(response => {
        // Handle response data, show success message, etc.
        console.log('Tickets created successfully:', response.data);
        alert(`Tickets creados para el cliente con ID ${customerId}!\nNúmero de Entradas: ${this.tickets}\nPrecio Total: €${this.tickets * this.ticketPrice}`);
      })
      .catch(error => {
        console.error('Error creating tickets:', error);
        alert('Hubo un problema al crear los tickets. Por favor, inténtelo de nuevo.');
      });
    }
  }
};
</script>

<style scoped>
@import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css');

.back {
  text-align: center;
  background: url('@/assets/backmobile.jpg') no-repeat center left scroll;
  background-size: cover;
  color: white;
  padding: 20px;
  min-height: 100vh; /* Cambiado a min-height para permitir expansión */
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.container {
  text-align: center;
  color: white;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
  flex: 1;
}

header {
  margin-top: 0px;
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
  padding: 20px;
  margin: 0 auto;
  max-width: 325px;
  text-align: center;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  margin-top: 10px;
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
  margin-bottom: 20px; /* Add margin below the countdown */
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
  margin: 1px 0;
}

.form-group {
  margin: 20px 0;
  text-align: center;
}

label {
  display: block;
  margin-bottom: 10px;
  font-weight: bold;
}

input[type="number"] {
  width: 50%;
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
  margin-top: 15px;
}

button:hover {
  background-color: #45a049;
}

footer {
  margin-top: 10px;
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
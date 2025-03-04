<template>
    <div class="container">
      <h1>Formulario de Pago</h1>
      <form @submit.prevent="enviarPago">
        <div>
          <label for="cedula">Cédula</label>
          <input type="text" id="cedula" v-model="formData.cedula"  required />
        </div>
  
        <div>
          <label for="nombre">Nombre</label>
          <input type="text" id="nombre" v-model="formData.nombre"  required />
        </div>
  
        <div>
          <label for="monto">Monto</label>
          <input type="number" id="monto" v-model="formData.monto"  required />
        </div>
  
        <div>
          <label for="cuentaBancaria">Cuenta Bancaria</label>
          <input type="text" id="cuentaBancaria" v-model="formData.cuentaBancaria"  required />
        </div>
  
        <div>
          <label for="tipoMoneda">Tipo de Moneda</label>
          <input type="text" id="tipoMoneda" v-model="formData.tipoMoneda"  required />
        </div>
  
        <div>
          <label for="fechaPago">Fecha de Pago</label>
          <input type="date" id="fechaPago" v-model="formData.fechaPago"  required />
        </div>
  
        <button type="submit" class="btn btn-primary mt-3">Enviar Pago</button>
      </form>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'

  
  const formData = ref({
    cedula: '',
    nombre: '',
    monto: '',
    cuentaBancaria: '',
    tipoMoneda: '',
    fechaPago: ''
  })
  
  const enviarPago = async () => {
    try {
      const response = await $fetch('http://localhost:3200/pagos', {
        method: 'POST',
        body: JSON.stringify(formData.value)
      })
      if (response) {
        formData.value = {
            nombre:'',
            monto:'',
            cuentaBancaria:'',
            tipoMoneda:'',
            fechaPago:'',
            cedula:'',

        }
        alert('Pago enviado con éxito')
      } else {
        alert('Hubo un error al enviar el pago: ')
      }
    } catch (error) {
      alert('Error de conexión: ' + error.message)
    }
  }
  </script>
    <style scoped>
  .container {
    max-width: 600px;
    margin: 0 auto;
  }
  </style>
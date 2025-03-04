<template>
    <div class="container">
      <h1>Registrar Empleado</h1>
      <form @submit.prevent="submitForm">
        <div class="form-group">
          <label for="firstName">Nombre</label>
          <input
            type="text"
            id="firstName"
            v-model="formData.FirstName"
            class="form-control"
            required
          />
        </div>
  
        <div class="form-group">
          <label for="lastName">Apellido</label>
          <input
            type="text"
            id="lastName"
            v-model="formData.LastName"
            class="form-control"
            required
          />
        </div>
  
        <div class="form-group">
          <label for="idNumber">Cédula</label>
          <input
            type="text"
            id="idNumber"
            v-model="formData.IDNumber"
            class="form-control"
            required
          />
        </div>
  
        <div class="form-group">
          <label for="salary">Salario</label>
          <input
            type="number"
            id="salary"
            v-model="formData.Salary"
            step="0.01"
            class="form-control"
            required
          />
        </div>
  
        <div class="form-group">
          <label for="department">Departamento</label>
          <input
            type="text"
            id="department"
            v-model="formData.Department"
            class="form-control"
            required
          />
        </div>
  
        <div class="form-group">
          <label for="jobTitle">Cargo</label>
          <input
            type="text"
            id="jobTitle"
            v-model="formData.JobTitle"
            class="form-control"
            required
          />
        </div>
  
        <div class="form-group">
          <label for="hireDate">Fecha de Contratación</label>
          <input
            type="date"
            id="hireDate"
            v-model="formData.HireDate"
            class="form-control"
            required
          />
        </div>
  
        <button type="submit" class="btn btn-primary mt-3">Enviar</button>
      </form>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const formData = ref({
    FirstName: '',
    LastName: '',
    IDNumber: '',
    Salary: '',
    Department: '',
    JobTitle: '',
    HireDate: '',
  });
  
  const submitForm = async () => {
    try {
      const  data  = await useFetch('https://localhost:7179/RHIntegration/send-to-tss', {
        method: 'POST',
        body: JSON.stringify(formData.value),
        headers: {
          'Content-Type': 'application/json',
        },
      });
  
      if (data) {
        alert('Empleado registrado con éxito');
        console.log(data.value);
      } 
    } catch (err) {
      alert('Error de conexión: ' + err.message);
    }
  };
  </script>
  
  <style scoped>
  .container {
    max-width: 600px;
    margin: 0 auto;
  }
  
  .form-group {
    margin-bottom: 15px;
  }
  </style>
  
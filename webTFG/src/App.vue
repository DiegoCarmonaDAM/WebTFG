<template>
  <div class="container">
    <h1>Registro de Usuarios</h1>

    <form @submit.prevent="login">
      <div class="input-group">
        <label>Correo</label>
        <input type="email" v-model="correo" placeholder="correo@email.com" />
      </div>

      <div class="input-group">
        <label>Contraseña</label>
        <input type="password" v-model="pass" placeholder="********" />
      </div>

      <button type="submit">Entrar</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import axios from 'axios'

const correo = ref('')
const pass = ref('')

async function login() {
  try {
    const response = await axios.post(
      "http://localhost:5034/api/auth/login", // 🔹 usa exactamente este URL
      {
        correo: correo.value,
        pass: pass.value
      }
    );

    alert(`¡Login correcto! Bienvenido ${response.data.user}`);
  } catch (error) {
    alert(error.response?.data?.message || "Login incorrecto");
  }
}

</script>

<style>
body{
  font-family: Arial, Helvetica, sans-serif;
  background:#f2f2f2;
}

.container{
  width:350px;
  margin:100px auto;
  padding:30px;
  background:white;
  border-radius:10px;
  box-shadow:0 0 10px rgba(0,0,0,0.1);
}

h1{
  text-align:center;
}

.input-group{
  margin-bottom:15px;
  margin-right: 20px;
}

input{
  width:100%;
  padding: 10px;
  margin-top:5px;
  border:1px solid #ccc;
  border-radius:5px;
}

button{
  width:100%;
  padding:10px;
  background:#42b883;
  color:white;
  border:none;
  border-radius:5px;
  cursor:pointer;
}

button:hover{
  background:#369f6b;
}
</style>
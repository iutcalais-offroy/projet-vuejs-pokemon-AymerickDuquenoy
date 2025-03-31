<script setup>
import { ref } from 'vue';
import axios from 'axios';

// Declare reactive variables
const email = ref('');
const password = ref('');
const signupPassword = ref('');
const confirmPassword = ref('');

const inscription = async () => {
  if (signupPassword.value !== confirmPassword.value) {
    console.error("Les mots de passe ne correspondent pas.");
    return;
  }

  try {
    const response = await axios.post('https://pokemon-api-seyrinian-production.up.railway.app/users', {
      email: email.value,
      password: signupPassword.value,
    });
    console.log('Inscription réussie', response.data);
  } catch (error) {
    console.error('Erreur lors de l\'inscription:', error);
  }
};

const login = async () => {
  try {
    const response = await axios.post('https://pokemon-api-seyrinian-production.up.railway.app/users/login', {
      email: email.value,
      password: password.value,
    });
    console.log('Connexion réussie', response.data);
  } catch (error) {
    console.error('Erreur lors de la connexion', error);
  }
};
</script>

<template>
  
</template>
<template>
  <n-card>
    <n-tabs
      class="card-tabs"
      default-value="signin"
      size="large"
      animated
      pane-wrapper-style="margin: 0 -4px"
      pane-style="padding-left: 4px; padding-right: 4px; box-sizing: border-box;"
    >
      <!-- Sign-in Tab -->
      <n-tab-pane name="signin" tab="Connexion">
        <n-form>
          <n-form-item-row label="Email">
            <n-input v-model:value="email" />
          </n-form-item-row>
          <n-form-item-row label="Mot de passe">
            <n-input type="password" v-model:value="password" />
          </n-form-item-row>
        </n-form>
        <!-- Pass the function directly to the @click event handler -->
        <n-button type="primary" block secondary strong @click="login">
          Connexion
        </n-button>
      </n-tab-pane>

      <!-- Sign-up Tab -->
      <n-tab-pane name="signup" tab="Inscription">
        <n-form>
          <n-form-item-row label="Email">
            <n-input v-model:value="email" />
          </n-form-item-row>
          <n-form-item-row label="Mot de passe">
            <n-input type="password" v-model:value="signupPassword" />
          </n-form-item-row>
          <n-form-item-row label="Confirmer votre mot de passe">
            <n-input type="password" v-model:value="confirmPassword" />
          </n-form-item-row>
        </n-form>
        <!-- Pass the function directly to the @click event handler -->
        <n-button type="primary" block secondary strong @click="inscription">
          Inscription
        </n-button>
      </n-tab-pane>
    </n-tabs>
  </n-card>
</template>

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
    window.location.reload();
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
    localStorage.token = response.data.token;
    window.location.href='/deck-builder'
  } catch (error) {
    console.error('Erreur lors de la connexion', error);
  }
};
</script>

<style scoped>
.card-tabs .n-tabs-nav--bar-type {
  padding-left: 4px;
}
</style>

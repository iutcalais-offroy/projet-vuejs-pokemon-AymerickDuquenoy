<template>
  <n-card content-style="padding: 0;">
    <n-tabs
      type="line"
      size="large"
      :tabs-padding="20"

    >
      <!-- Connexion Tab -->
      <n-tab-pane name="Connexion">
        <div class="form-group">
          <p>Email</p>
          <n-input
            v-model="email"
            placeholder="Entrez votre email"
            type="email"
          />
        </div>
        <div class="form-group">
          <p>Mot de passe</p>
          <n-input
            v-model="password"
            placeholder="Entrez votre mot de passe"
            type="password"
          />
        </div>
        <n-space justify="center">
          <n-button type="primary">Se connecter</n-button>
        </n-space>
      </n-tab-pane>
      
      <!-- Inscription Tab -->
      <n-tab-pane name="Inscription">
        <div class="form-group">
          <p>Email</p>
          <n-input
            v-model="email"
            placeholder="Entrez votre email"
            type="email"
          />
        </div>
        <div class="form-group">
          <p>Mot de passe</p>
          <n-input
            v-model="password"
            placeholder="Entrez votre mot de passe"
            type="password"
          />
        </div>
        <div class="form-group">
          <p>Confirmer le mot de passe</p>
          <n-input
            v-model="password"
            placeholder="Confirmez votre mot de passe"
            type="password"
          />
        </div>
        <n-space justify="center">
          <n-button type="primary">S'inscrire</n-button>
        </n-space>
      </n-tab-pane>
    </n-tabs>
  </n-card>
</template>

<script setup>
  import { ref } from 'vue';

  const email = ref("");
  const password = ref("");
</script>

<style scoped>
  .form-group {
    margin-bottom: 20px;
  }

  .n-input {
    width: 100%;
  }

  .n-button {
    width: 100%;
  }
</style>

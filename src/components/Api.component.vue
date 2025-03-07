<script setup>
import axios from 'axios';
async Inscription() {
      if (this.signupPassword !== this.confirmPassword) {
        console.error("Les mots de passe ne correspondent pas.");
        return;
      }

      try {
        const response = await axios.post('https://pokemon-api-seyrinian-production.up.railway.app/users', {
          email: this.email,
          password: this.password,
        });
        console.log('Inscription réussie', response.data);
      } catch (error) {
        console.error('Erreur lors de l\'inscription:', error);
      }
    },
  },
};

async Login(){
    
    try{
        const response = await axios.post('https://pokemon-api-seyrinian-production.up.railway.app/users/login'),
        {
            email: this.email,
            password: this.password,
        });
        console.log('Connexion réussie');
    }catch (error){
        console.error('Erreur lors de l\' connexion',error);
    }
    }
}
</script>

<template>
    
</template>


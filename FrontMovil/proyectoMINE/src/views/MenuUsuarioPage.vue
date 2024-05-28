<!-- src/views/MenuUsuario.vue -->
<template>
    <ion-page>
      <ion-header>
        <ion-toolbar>
          <ion-title>Bienvenido a Chefsito</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-content class="ion-padding">
        <ion-grid>
          <ion-row class="ion-justify-content-center ion-text-center">
            <ion-col size="12">
              <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRgP63uHFQ-qH3M5A8FFLM3w3SLHAn_fCVePhRDTq1eQg&s" alt="Logo Chefsito" class="logo" style="border-radius: 50%"/>
            </ion-col>
          </ion-row>
          <ion-row>
            <ion-col>
              <ion-button expand="block" @click="navigateTo('usuario1')" color="success" shape="round">Ver Recetas</ion-button>
            </ion-col>
          </ion-row>
          <ion-row>
            <ion-col>
              <ion-button expand="block" @click="navigateTo('planes')" color="success" shape="round">Ver Planes de Comidas</ion-button>
            </ion-col>
          </ion-row>
        </ion-grid>
      </ion-content>
    </ion-page>
  </template>
  
  <script setup lang="ts">
  import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonGrid, IonRow, IonCol, IonButton } from '@ionic/vue';
  import { useRouter } from 'vue-router';
  
  const router = useRouter();
  
  const navigateTo = (path: string) => {
    router.push({ path: `/${path}` });
  };
  </script>
  
  <style scoped>
  ion-header {
    --background: #32d296;
    --color: white;
  }
  
  .logo {
    width: 200px;
    height: auto;
    margin-top: 20px;
  }
  
  ion-button {
    margin: 20px 0;
    --border-radius: 20px;
    --padding-start: 16px;
    --padding-end: 16px;
  }
  
  ion-content {
    --background: #090909;
  }
  
  ion-grid {
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
  </style>
  
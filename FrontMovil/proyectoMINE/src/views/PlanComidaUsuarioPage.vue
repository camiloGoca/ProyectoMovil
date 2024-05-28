<!-- src/views/ListaPlanesUsuario.vue -->
<template>
    <ion-page>
      <ion-header>
        <ion-toolbar>
          <ion-title>Planes de Comida</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-content class="ion-padding">
        <ion-list>
          <ion-item v-for="plan in planesDeComida" :key="plan.id" @click="verDetalles(plan.id)">
            <ion-label>
              <h2>{{ plan.nombre }}</h2>
              <p>{{ plan.fechaInicio }} - {{ plan.fechaFin }}</p>
            </ion-label>
          </ion-item>
        </ion-list>
        <ion-row>
          <ion-col>
            <ion-button expand="full" color="success" @click="navigateTo('menuusuario')">Ir al Inicio</ion-button>
          </ion-col>
        </ion-row>
      </ion-content>
    </ion-page>
   
  </template>
  
  <script setup lang="ts">
  import { ref, onMounted } from 'vue';
  import { useRouter } from 'vue-router';
  import axios from '../axios';
  import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonList, IonItem, IonLabel } from '@ionic/vue';
  
  const router = useRouter();
  const planesDeComida = ref([]);
  
  const obtenerPlanesDeComida = async () => {
    try {
      const response = await axios.get('/planDeComida/get');
      planesDeComida.value = response.data;
    } catch (error) {
      console.error('Error al obtener los planes de comida:', error);
    }
  };
  
  const verDetalles = (id) => {
    router.push({ path: `/detalles-plan/${id}` });
  };

  const navigateTo = (path) => {
  router.push({ path: `/${path}` });
};
  
  onMounted(() => {
    obtenerPlanesDeComida();
  });
  </script>
  
  <style scoped>
  ion-header {
    --background: #32d296;
    --color: rgb(12, 12, 12);
  }
  
  ion-label h2 {
    color: #32d296;
    margin: 0;
  }
  
  ion-item {
    --background: #32383e;
    --border-radius: 10px;
    margin: 5px 0;
  }
  </style>
  
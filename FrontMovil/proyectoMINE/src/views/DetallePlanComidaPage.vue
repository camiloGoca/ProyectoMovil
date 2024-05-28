<!-- src/views/DetallesPlan.vue -->
<template>
    <ion-page>
      <ion-header>
        <ion-toolbar>
          <ion-title>Detalles del Plan de Comida</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-content class="ion-padding">
        <ion-card>
          <ion-card-header>
            <ion-card-title>{{ planDeComida.nombre }}</ion-card-title>
          </ion-card-header>
          <ion-card-content>
            <p><strong>Fecha Inicio:</strong> {{ planDeComida.fechaInicio }}</p>
            <p><strong>Fecha Fin:</strong> {{ planDeComida.fechaFin }}</p>
            <h2>Recetas</h2>
            <ion-list>
              <ion-item v-for="receta in planDeComida.recetas" :key="receta.id">
                <ion-label>{{ receta.nombre }}</ion-label>
              </ion-item>
            </ion-list>
          </ion-card-content>
        </ion-card>
      </ion-content>
    </ion-page>
  </template>
  
  <script setup lang="ts">
  import { ref, onMounted } from 'vue';
  import { useRoute } from 'vue-router';
  import axios from '../axios';
  import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonCard, IonCardHeader, IonCardTitle, IonCardContent, IonList, IonItem, IonLabel } from '@ionic/vue';
  
  const route = useRoute();
  const planDeComida = ref({
    nombre: '',
    fechaInicio: '',
    fechaFin: '',
    recetas: []
  });
  
  const obtenerPlanDeComida = async (id) => {
    try {
      const response = await axios.get(`/planDeComida/get/${id}`);
      planDeComida.value = response.data;
    } catch (error) {
      console.error('Error al obtener los detalles del plan de comida:', error);
    }
  };
  
  onMounted(() => {
    const id = route.params.id;
    obtenerPlanDeComida(id);
  });
  </script>
  
  <style scoped>
  ion-header {
    --background: #063c28;
    --color: rgb(119, 78, 78);
  }
  
  ion-card-title {
    color: #32d296;
  }
  
  ion-card {
    --background: #32383e;
    --border-radius: 10px;
    margin: 10px 0;
  }
  </style>
  
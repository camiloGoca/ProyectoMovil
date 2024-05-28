<template>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Recetas</ion-title>
      </ion-toolbar>
      <ion-toolbar>
        <ion-searchbar placeholder="Buscar"  v-model="filtro" @input="filtrarNombre"></ion-searchbar>
      </ion-toolbar>
    </ion-header>
    <ion-content fullscreen>
      <!-- Mostrar datos -->
      <div class="table-container">
        <ion-list>
          <!-- Iterar sobre items para mostrar los datos en tarjetas -->
          <ion-card v-for="(item, index) in items" :key="index" class="card-width">
            <ion-card-content>
              <ion-item>
                <ion-label class="label-header">Receta: </ion-label>
                <ion-label>{{ item.id }}</ion-label>
              </ion-item>
              <ion-item>
                <ion-label class="label-header">Nombre: </ion-label>
                <ion-label>{{ item.nombre }}</ion-label>
              </ion-item>
              <ion-item>
                <ion-label class="label-header">Descripcion: </ion-label>
                <ion-label>{{ item.descripcion }}</ion-label>
              </ion-item>
              <ion-item>
                <ion-label class="label-header">Instrucciones: </ion-label>
                <ion-label>{{ item.instrucciones }}</ion-label>
              </ion-item>
              <ion-item>
                <ion-label class="label-header">Tiempo de preparacion: </ion-label>
                <ion-label>{{ item.tiempoDePreparacion }}</ion-label>
              </ion-item>
              <ion-item>
                <ion-label class="label-header">Dificultad: </ion-label>
                <ion-label>{{ item.dificultad }}</ion-label>
              </ion-item>
              <ion-item>
                <ion-label class="label-header">Categoria: </ion-label>
                <ion-label>{{ item.categoria }}</ion-label>
              </ion-item>
              <ion-item v-for="(ingrediente, i) in item.ingredientes" :key="i" class="ingredient-item">
              <ion-item><ion-label>Ingredientes: </ion-label></ion-item>
              <ion-label>{{ ingrediente.nombre }}</ion-label>
            </ion-item>
           </ion-card-content>
          </ion-card>
        </ion-list>
      </div>
    </ion-content>
  </template>
  
  <script lang="ts">
  import { defineComponent, onMounted, ref, computed } from 'vue';
  import {
    IonHeader,
    IonSearchbar,
    IonTitle,
    IonToolbar,
    IonContent,
    IonList,
    IonCard,
    IonCardContent,
    IonItem,
    IonLabel
  } from '@ionic/vue';
  import axios from 'axios';
  
  export default defineComponent({
    components: {
      IonHeader,
      IonSearchbar,
      IonTitle,
      IonToolbar,
      IonContent,
      IonList,
      IonCard,
      IonCardContent,
      IonItem,
      IonLabel
    },
    setup() {
      const baseURL = 'http://localhost:9000/ProyectoDemo/receta';
      const items = ref<Array<ItemType>>([]);
      
      interface IngredienteType{
        id: number;
        nombre: string;
      }

      const filtro = ref('');

      interface ItemType {
        id: string;
        nombre: string;
        descripcion: string;
        instrucciones: string;
        tiempoDePreparacion: string;
        dificultad: string;
        categoria: string;
        ingredientes: Array<IngredienteType>;
      };
  
      onMounted(async () => {
        await findAllRecords();
      });
  
      async function findAllRecords() {
        try {
          const response = await axios.get(baseURL+'/get',{
            withCredentials: false
          });
          items.value = response.data;
          console.log(items.value); 
        } catch (error) {
          console.error('Error al obtener todos los registros:', error);
          throw error;
        }
      }

      const filtrarNombre = async () => {
        try {
            if (!filtro.value) {
                await findAllRecords();
            } else {
                const response = await axios.get(`${baseURL}/get`, {
                params: {
                nombre: filtro.value
                },
                withCredentials: false
        });
      items.value = response.data.filter(item => item.nombre === filtro.value);
      console.log(items.value); // Verifica que los datos sean correctos
    }
  } catch (error) {
    console.error('Error al filtrar por nombre:', error);
    throw error;
  }
};

      return {
        items,filtrarNombre, filtro
      };
    }
  });
  </script>
  
  <style scoped src="../theme/variables.css"></style>
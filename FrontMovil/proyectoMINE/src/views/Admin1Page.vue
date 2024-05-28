<!-- src/views/Admin1Page.vue -->
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Administrador</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
      <ion-grid>
        <ion-row>
          <ion-col class="ion-text-center">
            <h1>Hola Administrador</h1>
          </ion-col>
        </ion-row>
        <ion-row>
          <ion-col class="ion-text-center">
            <h2>¿Qué desea hacer hoy?</h2>
          </ion-col>
        </ion-row>
        <ion-row>
          <ion-col>
            <ion-button expand="block" @click="navigateTo('agregar-receta')" color="success" shape="round">Agregar Receta</ion-button>
          </ion-col>
        </ion-row>
        <ion-row>
          <ion-col>
            <ion-button expand="block" @click="navigateTo('admincinco')" color="success" shape="round">Agregar Plan De Comidas</ion-button>
          </ion-col>
        </ion-row>
        <ion-row>
          <ion-col>
            <ion-button expand="block" @click="navigateTo('lista-recetas')" color="success" shape="round">Ver Lista De Recetas</ion-button>
          </ion-col>
        </ion-row>
        <ion-row>
          <ion-col>
            <ion-button expand="block" @click="navigateTo('lista-planes')" color="success" shape="round">Ver Lista De Planes De Comida</ion-button>
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
  --background: #e9efed;
  --color: white;
}

h1, h2 {
  margin: 0;
  padding: 10px 0;
  color: #f9fffd;
}

ion-button {
  margin: 10px 0;
  --border-radius: 20px;
  --padding-start: 16px;
  --padding-end: 16px;
}

ion-content {
  --background: #0b0b0b;
}

ion-grid {
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

ion-col.ion-text-center {
  margin-bottom: 20px;
}
</style>

<template>
    <ion-page>
      <ion-card>
        <ion-card-header>
          Bienvenido Administrador
        </ion-card-header>
  
        <ion-card-content>
          Como tipo Administrador tienes muchas funcionalidades mas.
        </ion-card-content>
  
        <ion-button @click="RedirecScannerQR">Scannear</ion-button>
      </ion-card>
    </ion-page>
  </template>
  
  <script>
  import {IonPage, IonCardHeader, IonCard, IonCardContent, IonButton} from '@ionic/vue';
  
  export default {
    name: 'HomeAdminComponente',
    components: {
      IonPage, 
      IonCardHeader, 
      IonCard, 
      IonCardContent,
      IonButton
    },
    methods: {
      RedirecScannerQR() {
        this.$router.push('/scanner');
      },
  
      
  
  
    }
  }
  </script>
  
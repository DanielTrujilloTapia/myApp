<template>
    <ion-page>
      <ion-header>
      </ion-header>
      <ion-content>
        <div class="container-camara">
          <qrcode-stream @detect="onDetect"></qrcode-stream>
        </div>
        <ion-card>
          <ion-card-header>
            <ion-card-title>Códigos QR detectados:</ion-card-title>
          </ion-card-header>
          <ion-card-content>
            <ul>
              <li v-for="(code, index) in qrCodes" :key="index">
                {{ code }}
              </li>
            </ul>
          </ion-card-content>
        </ion-card>

        <router-link to="/home">
            <ion-button>Inicio</ion-button>
        </router-link>
        

      </ion-content>
    </ion-page>
  </template>
  
  <script setup>
  import { IonPage, IonHeader, IonContent, IonCard, IonCardHeader, IonCardTitle, IonCardContent, IonButton } from '@ionic/vue';
  import {RouterLink} from 'vue-router'
  import { QrcodeStream } from 'vue-qrcode-reader';
  import {ref} from 'vue';
  
  const qrCodes = ref([]);
  
  const onDetect = (detectedCodes) => {
    detectedCodes.forEach(code => {
      qrCodes.value.push(code.rawValue);
      console.log(code.rawValue);
    });
  };
  </script>
  
  <style>
  li {
    color: aliceblue;
  }
  
  .container-camara {
    display: flex;
    justify-content: center;
    align-items: flex-start;
    height: 100%;
    width: 100%;
    max-width: 400px;
    max-height: 400px;
    margin: 0 auto;
    padding-top: 20px;
  }
  </style>
  
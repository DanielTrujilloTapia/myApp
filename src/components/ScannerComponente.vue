<template>
    <ion-page>
      <div>
        <qrcode-stream @detect="onDetect"></qrcode-stream>
        <div>
          <h2>Códigos QR detectados:</h2>
          <ul>
            <li v-for="(code, index) in qrCodes" :key="index">
              {{ code }}
            </li>
          </ul>
        </div>
      </div>
    </ion-page>
  </template>
  
  <script setup>
  import { IonPage } from '@ionic/vue';
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
  
  .fixed-camera {
    width: 100vw; /* Ocupa el 100% del ancho de la pantalla */
    height: 50vh; /* Ocupa el 50% de la altura de la pantalla */
  }
  </style>
  
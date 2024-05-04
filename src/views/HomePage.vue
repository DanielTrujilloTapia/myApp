<template>
  <ion-page>
    <div>
      <qrcode-stream @decode="onDecode" @init="onInit"></qrcode-stream>
    </div>
  </ion-page>
</template>

<script setup>
import { IonPage } from '@ionic/vue';
import { QrcodeStream } from 'vue-qrcode-reader';

const onDecode = (result) => {
  console.log('QR code result:', result);
};

const onInit = (promise) => {
  promise.then(() => {
    console.log('Camera is ready');
  })
  .catch((error) => {
    console.error('Could not initialize camera', error);
  });
};
</script>

<style>
/* Aquí puedes añadir tus estilos */
</style>
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
import { ref } from 'vue';

const qrCodes = ref([]);

const onDetect = (detectedCodes) => {
  qrCodes.value.push(...detectedCodes);
};
</script>

<style>
li{
  color: aliceblue;
  
}
</style>

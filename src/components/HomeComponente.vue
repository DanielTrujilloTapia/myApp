<template>
  <ion-page>
    <ion-card>
      <ion-card-header>
        Deseas scannear codigos QR??
      </ion-card-header>

      <ion-card-content>
        Esta app nos permite scannear codigos QR y agg a una lista o contenedor que desees.
      </ion-card-content>

      <ion-button @click="RedirecScannerQR">Scannear</ion-button>
    </ion-card>
  </ion-page>
</template>

<script>
import {IonPage, IonCardHeader, IonCard, IonCardContent, IonButton} from '@ionic/vue';

export default {
  name: 'HomeComponente',
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
    }
  }
}
</script>

<template>
  <ion-page>
    <div class="container-login">
      <ion-card>
        <ion-card-header>
          <ion-img src="/usuario.png" class="header-image"></ion-img>
        </ion-card-header>
        <ion-card-content>
          <ion-list>
            <ion-item>
              <ion-label position="stacked">Nombre de usuario</ion-label>
              <ion-input v-model="username"></ion-input>
            </ion-item>
            <ion-item>
              <ion-label position="stacked">Contraseña</ion-label>
              <ion-input v-model="password" type="password"></ion-input>
            </ion-item>
          </ion-list>
          <ion-button expand="full" @click="login">Iniciar sesión</ion-button>
          <ion-button expand="full" @click="register">Registrarse</ion-button>
        </ion-card-content>
      </ion-card>
    </div>
  </ion-page>
</template>

<script >
import {IonPage, IonItem, IonList, IonLabel, IonInput, IonButton, IonImg, IonCard, IonCardContent, IonCardHeader } from '@ionic/vue';

export default {
  name:'LoginComponente',
  components:{
    IonPage,
    IonItem, 
    IonList, 
    IonLabel, 
    IonInput, 
    IonButton, 
    IonImg,
    IonCard,
    IonCardContent,
    IonCardHeader
  },
  data() {
    return {
      username: '',
      password: '',
    };
  },
  methods: {
    login() {
      if(this.username === 'admin' && this.password === 'admin'){
        this.$router.push('/home');
      }
    },
    register() {
      this.$router.push('/')
    }
  }
};
</script>

<style>
.header-image {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 40%;
}
.container-login{
  display: flex;
  justify-content: center;
  align-items: flex-start;
  height: 100%;
  width: 100%;
  max-width: 500px;
  margin: 0 auto;
  padding-top: 20px;
}
</style>

<template>
  <ion-page>
    <div class="container-login">
      <ion-card>
        <ion-card-header>
          <ion-img src="/usuario.png" class="header-image"></ion-img>
        </ion-card-header>
        <ion-card-content class="container-content">
          <ion-list>
            <ion-item>
              <ion-label position="stacked">Username:</ion-label>
              <ion-input v-model="username" required></ion-input>
            </ion-item>
            <ion-item>
              <ion-label position="stacked">Password:</ion-label>
              <ion-input v-model="password" type="password" required></ion-input>
            </ion-item>
          </ion-list>
          <div class="container-botones">
            <ion-button expand="full" @click="register" shape="round" fill="clear">Register</ion-button>
            <ion-button expand="full" @click="login" shape="round" fill="clear">Login</ion-button>
          </div>
          
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
    async login() {
      if (this.username !== '' && this.password !== '') {
        try {
          const response = await fetch('https://mysqlventapunto20240409001954.azurewebsites.net/api/Usu_Usuarios');
          const users = await response.json();
          const userFound = users.find((usu_usuario) => usu_usuario.nom_usuario === this.username && usu_usuario.contrasena === this.password);
          
          if (userFound) {
            console.log('Inicio de sesión exitoso');
            console.log('Estado del Usuario:', userFound.idusucatestado)
            
            localStorage.setItem('User-login', JSON.stringify(userFound)); //Guardo los datos del usuario que inicio sesion

            this.$router.push('/home');
          } else {
            console.log('Credenciales inválidas');
          }
        } catch (error) {
          console.error('Error al realizar la solicitud:', error);
        }
      } else {
        if (this.username === '') {
          console.log('Ingrese el USUARIO');
        }
        if (this.password === '') {
          console.log('Ingrese la CONTRASEÑA');
        }
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
.container-botones{
  display: flex;
  justify-content: center;
}
.container-login{
  display: flex;
  justify-content: center;
  align-items: flex-start;
  height: 100%;
  width: 100%;
  max-width: 250px;
  margin: 0 auto;
  padding-top: 20px;
}
</style>

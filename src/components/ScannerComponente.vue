<template>
  <ion-page>
    <ion-content>
      <ion-img src="/imgScanner.jpg" class="imagenQR" @click="openDialog"></ion-img>

      <div v-if="cameraActive" class="container-camara">
        <qrcode-stream @detect="onDetect"></qrcode-stream>
      </div>
      <div>
      <ion-button class="centered-button" @click="vaciarArreglos">Eliminar</ion-button>
    </div>

      <ion-card>
        <ion-card-header>
          <ion-card-title>Códigos QR detectados:</ion-card-title>
        </ion-card-header>
        <ion-card-content>
          <table>
            <thead>
              <tr>
                <th><ion-img src="/camion.jpg" class="iconos"></ion-img></th>
                <th><ion-img src="/tanqueimg.jpg" class="iconos"></ion-img></th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(item, index) in qrCodes.array1" :key="index" :class="{ 'highlight': qrCodes.array2[index] !== item, 'highlight-green': qrCodes.array2[index] === item}">
                <td class="center-text">{{ item }}</td>
                <td class="center-text">{{ qrCodes.array2[index] }}</td>
              </tr>
            </tbody>
          </table>
        </ion-card-content>
      </ion-card>

      <router-link to="/login">
          <ion-button>Login</ion-button>
      </router-link>
    </ion-content>
    <div v-if="dialogOpen" class="custom-dialog">
        <div class="dialog-content">
          <h4>Selecciona la parte a escanear</h4>
          <div class="iconos-container">
            <ion-img src="/camion.jpg" class="iconos" @click="selectArray(1)"></ion-img>
            <ion-img src="/tanqueimg.jpg" class="iconos" @click="selectArray(2)"></ion-img>
          </div>
        </div>
      </div>
  </ion-page>
</template>

<script setup>
import { ref } from 'vue';
import { IonPage, IonContent, IonButton, IonCard, IonCardContent, IonCardHeader, IonCardTitle, IonImg} from '@ionic/vue';
import { QrcodeStream } from 'vue-qrcode-reader';

const qrCodes = ref({ array1: [], array2: [] });
const cameraActive = ref(false);
const dialogOpen = ref(false);
const selectedArray = ref('array1');
let x=0;

const Userlogin = localStorage.getItem('User-login');
const UserLoginData = JSON.parse(Userlogin);

const onDetect = (detectedCodes) => {
  detectedCodes.forEach(code => {
    qrCodes.value[selectedArray.value].push(code.rawValue);
  });
  // Cerrar la cámara después de detectar un código QR
  cameraActive.value = false;
  peticiones();
};

const openDialog = () => {
  dialogOpen.value = true;
};

const selectArray = (array) => {
  selectedArray.value = array === 1 ? 'array1' : 'array2';
  dialogOpen.value = false;
  // Abrir la cámara al seleccionar un array
  cameraActive.value = true;
};

const vaciarArreglos = () => {
  qrCodes.value.array1 = [];
  qrCodes.value.array2 = [];
};
let vali;

const peticiones = () => {
  for ( let i=0; i <qrCodes.value.array1.length; i++) {
    const elemento = qrCodes.value.array1[x];
    const elemento2 = qrCodes.value.array2[x];
    if(elemento==elemento2){
      vali="correcta";
    }else{
      vali="incorrecta";
    }
    console.log(x);
    if(qrCodes.value.array1[x]!=null && qrCodes.value.array2[x]!=null  ){
      console.log("hora de hacer fetch");
      console.log(vali);
      x=x+1;
      
      try {
        const fecha1 = new Date().toISOString(); // Obtener la fecha actual en formato ISO
        const id_usuario = UserLoginData.id_usuario;

        console.log(elemento);
        console.log(elemento2);
        console.log(vali);
        console.log(fecha1);
        console.log(id_usuario);

        fetch('https://localhost:7199/api/Scanner_Datos', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
            
          },
          body: JSON.stringify({
            pro_aditivo: elemento,
            contenedor: elemento2,
            validacion: vali,
            fecha: fecha1,
            id_user: id_usuario
          })
        })
          .then(response => {
            if (!response.ok) {
              throw new Error('Error en la solicitud'); // Manejo de errores si la solicitud falla
            }
            return response.json(); // Parsea la respuesta como JSON
          })
          .then(data => {
            console.log('Respuesta del servidor:', data); // Hace algo con la respuesta exitosa
          })
          .catch(error => {
            console.error('Error en la solicitud:', error); // Maneja errores de red o de otro tipo
          });
      } catch (error) {
        console.error('Error en el fetch:', error); // Maneja errores generados al hacer el fetch

        

      }

    }
  }
};

</script>

<style>
.custom-dialog {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.dialog-content {
  background-color: #fff;
  padding: 20px;
  border-radius: 10px;
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

table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  border: 1px solid #ddd;
  padding: 5px;
  text-align: left;
}

th {
  background-color: #f2f2f2;
}

.highlight {
  background-color: rgb(218, 131, 131);
  text-align: center;
  color: black;
}
.highlight-green{
  background-color: rgb(168, 235, 165);
  text-align: center;
  color: black;
}
.iconos {
  width: 40px;
  margin: 0 auto;
}

.iconos-container {
  display: flex;
  flex-direction: row; /* Alinear las imágenes en una fila */
}

.center-text {
  text-align: center;
}

.imagenQR{
  width: 300px;
  margin: 20px auto 0;
}

.centered-button {
  display: block;
  margin: 20px auto 0;
  width: 100px;
}

</style>
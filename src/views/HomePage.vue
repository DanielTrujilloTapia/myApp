<template>
  <home-componente v-if="userType === 2"/>
  <home-admin-componente v-else-if="userType === 1"/>
</template>
<script setup>
import HomeComponente from '../components/HomeComponente.vue'
import HomeAdminComponente from '../components/HomeAdminComponente.vue';

const Userlogin = localStorage.getItem('User-login');
const UserLoginData = JSON.parse(Userlogin);

const userType = UserLoginData ? UserLoginData.idusucattipousuario : null

</script>
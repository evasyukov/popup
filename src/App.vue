<template>
  <div id="app">
     <button @click="openPopup">Начать</button>
     <Popup ref="popup" />
  </div>
 </template>
 
 <script>
 import Popup from './components/Popup.vue';
 
 export default {
  components: {
     Popup,
  },
  methods: {
     openPopup() {
       this.$refs.popup.openPopup(); // this.$refs.popup используется для вызова метода openPopup
     },
  },
 };
 </script>
 

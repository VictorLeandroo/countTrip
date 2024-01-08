<template>
  <div id="app">
    <CountdownCustom />
  </div>
</template>

<script>
import CountdownCustom from './components/CountdownCustom.vue';


export default {
  components: {
    CountdownCustom,
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap');

#app{
  background-image: url('../public/assets/camping.png');
  width: 100vw;
  height: 100vh;
  background-size: cover;
  background-position: center;
  position: fixed;
  top: 0;
  left: 0;
  font-family: 'Roboto', sans-serif;
}

/* Adicione uma regra de mídia para ajustar a imagem em dispositivos móveis */
@media (max-width: 768px) {
  #app {
    background-image: url('../public/assets/camping2.jpg');
  }
}
</style>
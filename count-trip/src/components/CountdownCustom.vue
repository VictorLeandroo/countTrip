<template>
  <section class="contador" style="display: flex;">
    <div class="header">
      <h1>Faltam</h1>
    </div>
    <div class="wrapper">
      <div>
        <span id="days">{{ days }}</span>
        <span>Dias</span>
      </div>
      <div>
        <span id="hours">{{ hours }}</span>
        <span>Horas</span>
      </div>
      <div>
        <span id="minutes">{{ minutes }}</span>
        <span>Minutos</span>
      </div>
      <div>
        <span id="seconds">{{ seconds }}</span>
        <span>Segundos</span>
      </div>
    </div>
  </section>

  <div id="images" class="image-container">
    <img v-for="(image, index) in images" :key="index" :src="`/assets/${image.src}`"
      :style="{ animationDelay: `${index * 0.5}s` }" height="45" alt="" class="floating-image" />
  </div>
</template>

<script>
import moment from 'moment';
import axios from 'axios';

export default {
  data() {
    return {
      targetDate: moment('2024-01-13'),
      currentDate: moment(),
      images: [
        { src: 'victor.jpg' },
        { src: 'lala.jpg' },
        { src: 'dayra.jpg' },
        { src: 'lucas.jpg' },
        { src: 'nogueira.jpg' },
        { src: 'gabriel.jpg' },
        { src: 'simplicio.jpg' },
        { src: 'vitin.jpg' },
      ],

      weather: {},
    };
  },
  computed: {
    days() {
      return this.targetDate.diff(this.currentDate, 'days');
    },
    hours() {
      return this.targetDate.diff(this.currentDate, 'hours') % 24;
    },
    minutes() {
      return this.targetDate.diff(this.currentDate, 'minutes') % 60;
    },
    seconds() {
      return this.targetDate.diff(this.currentDate, 'seconds') % 60;
    },
  },

  methods: {
    async getWeather() {
      const apiKey = 'ca46ee1312eb7a8a0362c121b3e6b7b0';



      try {
        const response = await axios.get(
          `/api/v1/anl/synoptic/locale/:BR?token=${apiKey}`
        );
        this.weather = response.data;
      } catch (error) {
        console.error('Erro ao obter a previsão do tempo', error);
      }
    },
  },

  mounted() {
    setInterval(() => {
      this.currentDate = moment();
    }, 1000);
    this.getWeather();
  },
};
</script>

<style scoped>
#contador {
  display: flex;
  justify-content: center;
}

#images img {
  border-radius: 50%;
}

.image-container {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 25px;
  flex-wrap: wrap;
  height: 50%;
  margin-top: 119px;
}

.floating-image {
  animation: floatAnimation 5s ease-in-out infinite;
}

@keyframes floatAnimation {

  0%,
  100% {
    transform: translateY(0);
  }

  50% {
    transform: translateY(-10px);
  }
}

.wrapper {
  display: flex;
  justify-content: space-around;
  width: 100vw;
  padding-left: 10vw;
  padding-right: 10vw;
  margin-top: 20px;
}

.contador {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.contador div>span:nth-child(1) {
  color: white;
  font-size: 4rem;
}

.contador div>span:nth-child(2) {
  color: #ff0000;
  font-size: 1rem;
  font-weight: 800;
}

.wrapper div {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
<template>
  <div class="weather-fullscreen">
    <div class="week-selector">
      <button
        v-for="(day, index) in week"
        :key="day.name"
        :class="{ active: selectedDay === index }"
        @click="selectedDay = index"
      >
        {{ day.name }}
      </button>
    </div>

    <div class="weather-card">
      <div class="header">
        <h2>{{ city }}</h2>
        <div class="alert">⚠ Сейчас: Лесной пожар – Средний уровень</div>
      </div>

      <div class="main-info">
        <div class="left">
          <img :src="`/icons/${week[selectedDay].icon}`" alt="weather icon" />
          <div class="temperature-block">
            <h1 class="temp">{{ week[selectedDay].temp }}°C</h1>
            <p class="description">{{ week[selectedDay].description }}</p>
            <p class="feels">Ощущается как {{ week[selectedDay].feelsLike }}°</p>
          </div>
        </div>

        <div class="right">
          <p class="summary">{{ week[selectedDay].summary }}</p>
          <div class="details">
            <div><strong>Ветер:</strong> {{ week[selectedDay].wind }} м/с</div>
            <div><strong>Влажность:</strong> {{ week[selectedDay].humidity }}%</div>
            <div><strong>Видимость:</strong> {{ week[selectedDay].visibility }} км</div>
            <div><strong>Давление:</strong> {{ week[selectedDay].pressure }} мм</div>
            <div><strong>Точка росы:</strong> {{ week[selectedDay].dewPoint }}°</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const selectedDay = ref(0);
const city = 'Чебоксары, Чувашская Республика';

const week = [
  {
    name: 'Пн',
    temp: 21,
    feelsLike: 23,
    description: 'Небольшой дождь',
    summary: 'Ожидается значительная облачность. Макс. температура — 24°.',
    wind: 1,
    humidity: 100,
    visibility: 10,
    pressure: 755,
    dewPoint: 21,
    icon: 'rainy.svg',
  },
  {
    name: 'Вт',
    temp: 24,
    feelsLike: 25,
    description: 'Ясно',
    summary: 'Солнечно весь день.',
    wind: 2,
    humidity: 50,
    visibility: 10,
    pressure: 752,
    dewPoint: 17,
    icon: 'sunny.svg',
  },
  {
    name: 'Ср',
    temp: 22,
    feelsLike: 21,
    description: 'Облачно',
    summary: 'Местами облачно, возможен лёгкий дождь.',
    wind: 3,
    humidity: 70,
    visibility: 9,
    pressure: 753,
    dewPoint: 18,
    icon: 'cloudy.svg',
  },
  {
    name: 'Чт',
    temp: 19,
    feelsLike: 18,
    description: 'Дождь',
    summary: 'Ожидается дождь в течение дня.',
    wind: 4,
    humidity: 90,
    visibility: 8,
    pressure: 750,
    dewPoint: 19,
    icon: 'rainy.svg',
  },
  {
    name: 'Пт',
    temp: 23,
    feelsLike: 24,
    description: 'Переменная облачность',
    summary: 'Тёплая погода с переменной облачностью.',
    wind: 2,
    humidity: 60,
    visibility: 10,
    pressure: 754,
    dewPoint: 20,
    icon: 'partly-cloudy.svg',
  },
  {
    name: 'Сб',
    temp: 26,
    feelsLike: 27,
    description: 'Жарко',
    summary: 'Солнечно и жарко весь день.',
    wind: 1,
    humidity: 40,
    visibility: 10,
    pressure: 755,
    dewPoint: 18,
    icon: 'sunny.svg',
  },
  {
    name: 'Вс',
    temp: 20,
    feelsLike: 19,
    description: 'Прохладно',
    summary: 'Прохладный ветер, возможны облака.',
    wind: 3,
    humidity: 80,
    visibility: 9,
    pressure: 751,
    dewPoint: 17,
    icon: 'cloudy.svg',
  },
];
</script>

<style scoped>
/* Занимает весь экран */
.weather-fullscreen {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;

  background: linear-gradient(to top, #304acb, #1e2d90);
  color: white;
  display: flex;
  flex-direction: column;
  padding: 2rem;
  box-sizing: border-box;
  font-family: 'Segoe UI', sans-serif;
  overflow: hidden;
}

body {
  margin: 0;
  padding: 0;
  overflow: hidden;
}


/* Кнопки дней */
.week-selector {
  display: flex;
  justify-content: center;
  margin-bottom: 2rem;
  gap: 0.5rem;
  flex-wrap: wrap;
}
.week-selector button {
  padding: 0.6rem 1.2rem;
  border: none;
  background: #4564ff;
  color: white;
  border-radius: 8px;
  cursor: pointer;
  font-size: 1rem;
  transition: background 0.3s ease;
}
.week-selector button.active {
  background: #ffcc00;
  color: #000;
  font-weight: bold;
}

/* Карточка */
.weather-card {
  flex: 1;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 16px;
  padding: 2rem;
  display: flex;
  flex-direction: column;
}

/* Заголовок */
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 2rem;
}
.alert {
  background: #ffcc00;
  color: #333;
  padding: 0.5rem 1rem;
  border-radius: 8px;
  font-weight: bold;
}

/* Основная информация */
.main-info {
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;
  align-items: center;
}
.left {
  display: flex;
  align-items: center;
  gap: 1rem;
}
.left img {
  width: 80px;
  height: 80px;
}
.temperature-block {
  display: flex;
  flex-direction: column;
}
.temp {
  font-size: 4rem;
  font-weight: bold;
  margin: 0;
  line-height: 1;
}
.description {
  font-size: 1.5rem;
  color: #ffd;
  margin: 0.2rem 0;
}
.feels {
  font-size: 1rem;
  opacity: 0.9;
}

/* Правая часть */
.right {
  flex: 1;
}
.summary {
  font-size: 1.2rem;
  margin-bottom: 1rem;
}
.details {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
  gap: 0.8rem;
}
</style>

<template>
  <div class="weather-app">
    <div class="header">
      <select v-model="selectedCity" @change="changeCity" class="city-select">
        <option v-for="city in cities" :key="city">{{ city }}</option>
      </select>
    </div>

    <div class="main-weather">
      <div class="center-block">
        <img src="/icons/rainy.svg" alt="weather icon" class="weather-icon" />
        <div class="weather-text">
          <div class="temperature">{{ currentWeather.temp }}°C</div>
          <div class="condition">{{ currentWeather.condition }}</div>
          <div class="feels-like">Ощущается как {{ currentWeather.feels_like ?? currentWeather.temp }}°</div>
        </div>
      </div>
    </div>

    <div class="week-forecast">
      <div
        v-for="(day, index) in weekWeather"
        :key="index"
        class="day-card"
        :class="{ active: selectedDayIndex === index }"
        @click="selectDay(index)"
      >
        <div>{{ day.day }}</div>
        <div>{{ day.temp }}°</div>
      </div>
    </div>

    <div class="day-details" v-if="selectedDay">
      <h3>Подробности на {{ selectedDay.day }}</h3>
      <p><strong>Температура:</strong> {{ selectedDay.temp }}°C</p>
      <p><strong>Состояние:</strong> {{ selectedDay.condition }}</p>
      <p><strong>Ветер:</strong> {{ selectedDay.wind }} м/с</p>
      <p><strong>Влажность:</strong> {{ selectedDay.humidity }}%</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedCity: "Чебоксары",
      cities: ["Чебоксары", "Москва", "Санкт-Петербург", "Казань", "Екатеринбург"],
      weatherData: {
        "Чебоксары": {
          currentWeather: {
            temp: 21,
            condition: "Небольшой дождь",
            feels_like: 23,
            wind: 1,
            humidity: 100,
            visibility: 10,
            pressure: 755,
            dew_point: 21,
          },
          weekWeather: [
            { day: "Пн", temp: 21, condition: "Дождь", wind: 1, humidity: 90 },
            { day: "Вт", temp: 20, condition: "Облачно", wind: 2, humidity: 80 },
            { day: "Ср", temp: 19, condition: "Ясно", wind: 3, humidity: 70 },
            { day: "Чт", temp: 21, condition: "Дождь", wind: 1, humidity: 90 },
            { day: "Пт", temp: 23, condition: "Солнечно", wind: 2, humidity: 60 },
            { day: "Сб", temp: 18, condition: "Облачно", wind: 3, humidity: 75 },
            { day: "Вс", temp: 20, condition: "Ясно", wind: 1, humidity: 65 },
          ],
        },
        "Москва": {
          currentWeather: {
            temp: 25,
            condition: "Ясно",
            feels_like: 26,
            wind: 3,
            humidity: 50,
            visibility: 12,
            pressure: 760,
            dew_point: 15,
          },
          weekWeather: [
            { day: "Пн", temp: 25, condition: "Ясно", wind: 3, humidity: 50 },
            { day: "Вт", temp: 24, condition: "Облачно", wind: 4, humidity: 55 },
            { day: "Ср", temp: 23, condition: "Дождь", wind: 5, humidity: 70 },
            { day: "Чт", temp: 22, condition: "Ясно", wind: 3, humidity: 60 },
            { day: "Пт", temp: 26, condition: "Солнечно", wind: 2, humidity: 40 },
            { day: "Сб", temp: 27, condition: "Облачно", wind: 3, humidity: 50 },
            { day: "Вс", temp: 25, condition: "Ясно", wind: 4, humidity: 45 },
          ],
        },
        "Санкт-Петербург": {
          currentWeather: {
            temp: 18,
            condition: "Облачно",
            feels_like: 18,
            wind: 5,
            humidity: 80,
            visibility: 8,
            pressure: 754,
            dew_point: 16,
          },
          weekWeather: [
            { day: "Пн", temp: 18, condition: "Облачно", wind: 5, humidity: 80 },
            { day: "Вт", temp: 17, condition: "Дождь", wind: 6, humidity: 85 },
            { day: "Ср", temp: 16, condition: "Облачно", wind: 5, humidity: 78 },
            { day: "Чт", temp: 17, condition: "Ясно", wind: 4, humidity: 70 },
            { day: "Пт", temp: 18, condition: "Дождь", wind: 5, humidity: 80 },
            { day: "Сб", temp: 19, condition: "Облачно", wind: 5, humidity: 75 },
            { day: "Вс", temp: 18, condition: "Ясно", wind: 4, humidity: 70 },
          ],
        },
        "Казань": {
          currentWeather: {
            temp: 22,
            condition: "Ясно",
            feels_like: 22,
            wind: 2,
            humidity: 60,
            visibility: 10,
            pressure: 758,
            dew_point: 18,
          },
          weekWeather: [
            { day: "Пн", temp: 22, condition: "Ясно", wind: 2, humidity: 60 },
            { day: "Вт", temp: 21, condition: "Облачно", wind: 3, humidity: 65 },
            { day: "Ср", temp: 20, condition: "Дождь", wind: 3, humidity: 70 },
            { day: "Чт", temp: 21, condition: "Ясно", wind: 2, humidity: 60 },
            { day: "Пт", temp: 23, condition: "Солнечно", wind: 2, humidity: 55 },
            { day: "Сб", temp: 24, condition: "Облачно", wind: 3, humidity: 60 },
            { day: "Вс", temp: 22, condition: "Ясно", wind: 2, humidity: 60 },
          ],
        },
        "Екатеринбург": {
          currentWeather: {
            temp: 20,
            condition: "Облачно",
            feels_like: 19,
            wind: 4,
            humidity: 70,
            visibility: 9,
            pressure: 757,
            dew_point: 17,
          },
          weekWeather: [
            { day: "Пн", temp: 20, condition: "Облачно", wind: 4, humidity: 70 },
            { day: "Вт", temp: 19, condition: "Дождь", wind: 5, humidity: 75 },
            { day: "Ср", temp: 18, condition: "Облачно", wind: 4, humidity: 70 },
            { day: "Чт", temp: 20, condition: "Ясно", wind: 3, humidity: 65 },
            { day: "Пт", temp: 21, condition: "Солнечно", wind: 2, humidity: 60 },
            { day: "Сб", temp: 19, condition: "Облачно", wind: 3, humidity: 70 },
            { day: "Вс", temp: 20, condition: "Ясно", wind: 3, humidity: 65 },
          ],
        },
      },
      currentWeather: {},
      weekWeather: [],
      selectedDayIndex: 0,
    };
  },
  computed: {
    selectedDay() {
      return this.weekWeather[this.selectedDayIndex];
    },
  },
  mounted() {
    this.loadCityData(this.selectedCity);
  },
  methods: {
    changeCity() {
      this.loadCityData(this.selectedCity);
      this.selectedDayIndex = 0;
    },
    loadCityData(city) {
      const data = this.weatherData[city];
      if (data) {
        this.weekWeather = data.weekWeather;
        this.currentWeather = data.currentWeather;
        this.selectedDayIndex = 0;
      }
    },
    selectDay(index) {
      this.selectedDayIndex = index;
      const dayData = this.weekWeather[index];
      this.currentWeather = {
        temp: dayData.temp,
        condition: dayData.condition,
        feels_like: dayData.feels_like ?? dayData.temp,
        wind: dayData.wind,
        humidity: dayData.humidity,
        visibility: dayData.visibility ?? "—",
        pressure: dayData.pressure ?? "—",
        dew_point: dayData.dew_point ?? "—",
      };
    },
  },
};
</script>

<style scoped>

.weather-app {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  min-height: 100vh;
  width: 100vw;
  max-width: 1200px;
  margin: 0 auto;
  background: linear-gradient(to bottom, #1e3c72, #2a5298);
  color: white;
  padding: 20px;
  box-sizing: border-box;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
}

.city-select {
  background: rgba(255, 255, 255, 0.329);
  border: none;
  border-radius: 8px;
  padding: 8px 15px;
  color: rgb(29, 35, 48);
  font-size: 16px;
  cursor: pointer;
  transition: background 0.3s ease;
  appearance: none;
  background-repeat: no-repeat;
  background-position: right 10px center;
  background-size: 12px;
}

.city-select:hover {
  background: rgba(255, 255, 255, 0.3);
}

.city-select:focus {
  outline: none;
  background: rgba(255, 255, 255, 0.4);
}

.alert {
  font-weight: 600;
}

.main-weather {
  display: flex;
  justify-content: center;
  align-items: center;
  background: rgba(255, 255, 255, 0.1);
  padding: 20px;
  border-radius: 10px;
  margin-top: 20px;
}

.center-block {
  display: flex;
  align-items: center;
  gap: 25px;
}

.weather-icon {
  width: 80px;
  height: 80px;
}

.weather-text {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.temperature {
  font-size: 64px;
  font-weight: bold;
  line-height: 1;
}

.condition {
  font-size: 24px;
  margin-top: 5px;
}

.feels-like {
  font-size: 18px;
  margin-top: 5px;
}

.week-forecast {
  display: flex;
  justify-content: space-between;
  margin-top: 20px;
}

.day-card {
  background: rgba(255, 255, 255, 0.2);
  padding: 10px;
  border-radius: 8px;
  text-align: center;
  flex: 1;
  margin: 0 5px;
  cursor: pointer;
  user-select: none;
  transition: background 0.3s ease;
}

.day-card:hover {
  background: rgba(255, 255, 255, 0.35);
}

.day-card.active {
  background: #4a90e2;
  font-weight: bold;
}

.day-details {
  margin-top: 20px;
  background: rgba(255, 255, 255, 0.1);
  padding: 15px;
  border-radius: 10px;
}
</style>

<style>
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  width: 100%;
  overflow-x: hidden;
}

body {
  background: linear-gradient(to bottom, #1e3c72, #2a5298);
}
</style>
<template>
  <div
    id="app"
    :class="
      typeof weather.main != 'undefined' && weather.main.temp < 16 ? 'col' : ''
    "
  >
    <div class="weather">
      <div class="search">
        <input
          class="input"
          v-model="city"
          type="text"
          placeholder="Search City ..."
        />
        <button class="btn" @click="fetchFunction()" type="submit">
          Search
        </button>
      </div>
      <div class="weather-data" v-if="typeof weather.name != 'undefined'">
        <h1 class="title">{{ weather.name }} , {{ weather.sys.country }}</h1>
        <p class="date">{{ nowDate() }}</p>
        <button class="temp">{{ Math.round(weather.main.temp) }} °C</button>
        <p class="weathers">{{ weather.weather[0].main }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      api_keys: "2e54d6a7730153e86814e91537b237b8",
      base_url: "https://api.openweathermap.org/data/2.5/",
      city: "",
      weather: "",
    };
  },
  methods: {
    fetchFunction(e) {
      fetch(
        `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&APPID=2e54d6a7730153e86814e91537b237b8&units=metric`
      )
        .then((res) => {
          return res.json();
        })
        .then(this.setResults);
    },
    setResults(results) {
      this.weather = results;
    },
    nowDate() {
      let d = new Date();
      let days = [
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
        "Sunday",
      ];
      let months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      let month = months[d.getMonth()];
      let day = days[d.getDay()];
      let date = d.getDate();
      let year = d.getFullYear();
      return `${day},${date} ${month} ${year}`;
    },
  },
};
</script>

<style scoped>
#app {
  background-image: url("https://i.pinimg.com/564x/5f/99/61/5f99611c5d14b393612680ca7278bf86.jpg");
  background-size: cover;
  background-position: bottom;
  padding-top: 25px;
  padding-left: 15px;
  padding-right: 15px;
  transition: 0.45s;
}
#app.col {
  background-image: url("https://i.pinimg.com/236x/95/e4/54/95e454775f458d24614ccbf3d6e38c6c.jpg");
}
.weather {
  min-height: 96vh;
  min-width: 500px;
  box-shadow: 50px 40px 100px rgba(0, 0, 0, 0.75);
}
.title {
  margin: 0;
  margin-top: 15px;
  color: rgba(255, 255, 255, 0.75);
  text-align: center;
}
.input {
  padding: 9.5px 5px;
  font-size: 20px;
  font-weight: bold;
  border-radius: 0px 16px 0px 16px;
  width: 70%;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  background-color: rgba(255, 255, 255, 0.75);
  color: rgba(0, 0, 0, 0.75);
  box-shadow: 0 0 16px rgba(255, 255, 255, 0.75);
}
.search {
  display: flex;
  align-items: center;
  justify-content: baseline;
}
.input:focus {
  border-radius: 16x 0px 16px 0px;
}
.btn {
  width: 28%;
  margin-left: -20px;
  background-color: #2357bc;
  border-radius: 0 16px 0 0;
  color: rgba(255, 255, 255, 0.75);
}
.date {
  color: #fff;
  text-align: end;
  margin-right: 45px;
}
.temp {
  font-size: 25px;
  font-weight: bolder;
  display: block;
  text-align: right;
}
.weathers {
  font-size: 26px;
  line-height: 16px;
  font-weight: bold;
  color: rgba(255, 255, 255, 0.75);
  text-align: end;
  margin-right: 45px;
}
.date {
  font-style: italic;
}
</style>

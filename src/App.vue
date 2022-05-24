<template>
  <div class="App">
    <main>
      <div class="search-box">
        <div class="search-bar">
          <input
            type="text"
            class="form-control"
            placeholder="Enter city name..."
            v-model="query"
            @keypress="fetchWeather"
          />
        </div>
      </div>
      <div class="weather-box" v-if="typeof this.weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">
            {{ weather.name }}, {{ weather.sys.country }}
          </div>
          <div class="date">{{ getDate() }}</div>
        </div>
        <div class="temp-box">
          <div class="temp">
            {{ Math.round(weather.main.temp)
            }}<span class="celsius-sign">℃</span>
          </div>
          <div class="weather-discription">
            {{ weather.weather[0].description }}
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      api_key: "8542e44c9d5fe6fcd5ed9d628cfc11a1",
      url: "https://api.openweathermap.org/data/2.5/",
      api_call: "weather?q={city name}&units=metric&appid={API key}",
      query: "",
      weather: {},
    };
  },
  methods: {
    fetchWeather(e) {
      if (e.key == "Enter") {
        fetch(
          `${this.url}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
        )
          .then((res) => res.json())
          .then(this.setResults);
      }
    },
    setResults(results) {
      this.weather = results;
    },
    getDate() {
      let d = new Date();
      let months = [
        "Styczen",
        "Luty",
        "Marzec",
        "Kwiecien",
        "Maj",
        "Czerwiec",
        "Lipiec",
        "Sierpien",
        "Wrzesien",
        "Pazdziernik",
        "Listopad",
        "Grudzien",
      ];
      let days = [
        "Poniedzialek",
        "Wtorek",
        "Sroda",
        "Czwartek",
        "Piatek",
        "Sobota",
        "Niedziela",
      ];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return `${day},  ${date} ${month} ${year}`;
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Anton&family=Zen+Antique&display=swap");

* {
  font-family: "Zen Antique", serif;
}

:root {
  --my-grey: rgba(255, 255, 255, 0.8);
}

body {
  background-image: url(https://images.theconversation.com/files/232705/original/file-20180820-30593-1nxanpj.jpg?ixlib=rb-1.1.0&q=45&auto=format&w=1200&h=1200.0&fit=crop);
  background-size: cover;
  background-color: blue;
  background-blend-mode: screen;
}

.search-box {
  text-align: center;
}
.search-bar > input {
  color: var(--my-grey);
  background-color: rgba(55, 55, 55, 0.8);
  font-style: inherit;
  text-align: center;
  font-size: 22px;
  transition: all 0.5s ease;
  padding: 10px;
  margin: 10px 0;
  height: 5vh;
  width: 70vh;
  border: 3px solid grey;
  border-radius: 16px 0 16px 0;
  box-shadow: 0 0 15px 4px rgba(0, 0, 0, 0.6);
}
.search-bar > input::placeholder {
  color: var(--my-grey);
}
.search-bar > input:hover {
  transition: all 0.5s ease;
  border-radius: 16px 16px 16px 16px;
  cursor: pointer;
}
.search-bar > input:focus {
  color: var(--my-grey);
  outline-style: groove;
  transition: all 0.5s ease;
  border-radius: 16px 16px 16px 16px;
  text-align: center;
  border: 3px solid grey;
}

.weather-box {
  text-align: center;
  background-color: rgba(33, 33, 33, 0.7);
  width: 40vw;
  margin: 0 auto;
  padding: 15px;
  box-shadow: 0 0 15px 4px rgba(0, 0, 0, 0.4);

  border-radius: 8px 8px 8px 8px;
}

.location-box {
  padding: 5px 0;
  font-size: 25px;
  text-shadow: 3px 3px #444;
  margin: 10px;
  padding-top: 10px;
  color: var(--my-grey);
}

.temp-box {
  margin: 10px;
  font-size: 30px;
  font-family: "Anton", serif;
  color: var(--my-grey);
}
.temp-box > .temp {
  margin: 0 auto;
  border-radius: 12px;
  box-shadow: 0px 0px 58px 18px rgba(57, 57, 67, 1);
  width: 15vw;
  background-color: rgba(255, 255, 255, 0.2);
  font-size: 70px;
  text-shadow: 4px 4px #444;
}
.temp-box > .temp-discription {
  text-transform: lowercase;
}

.celsius-sign {
  font-size: 60px;
}
</style>

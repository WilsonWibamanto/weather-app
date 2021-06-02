<template>
  <div>
    <img
      class="absolute bg-cover filter brightness-50 bg-bottom h-full w-screen z-0"
      src="https://picsum.photos/1200/800?random=1"
    />
    <div class="relative pt-12 z-10 block justify-center">
      <h2 class="my-10">Weather Forecast Application</h2>
      <div>
        <SearchBar @enter="fetchData" @press="fetchData" />
      </div>

      <div
        class="justify-center items-center flex-col space-y-4 rounded-2xl mt-10 m-auto bg-black w-max bg-opacity-80 p-4"
        v-if="typeof weather.main != 'undefined'"
      >
        <p>{{ weather.name }} , {{ weather.sys.country }}</p>
        <div
          class="justify-center items-center w-max p-2 m-auto bg-white bg-opacity-30 rounded-lg"
        >
          <div class="flex space-x-4">
            <div class="flex-col p-2">
              <div>
                <h2>{{ Math.round(weather.main.temp) - 273 }}°C</h2>
              </div>
              <div>
                <label
                  >Min: {{ Math.round(weather.main.temp_min) - 273 }}°</label
                >
              </div>
              <div>
                <label
                  >Max: {{ Math.round(weather.main.temp_max) - 273 }}°</label
                >
              </div>
            </div>
            <div class="flex-col mx-auto mt-4">
              <div class="bg-white bg-opacity-50 rounded-md">
                <img :src="icon" />
              </div>
              <div class="justify-center items-center">
                <label>{{ description }}</label>
              </div>
            </div>
          </div>

          <br />
        </div>
        <div>
          <label class="italic">{{ dateBuilder() }}</label>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import SearchBar from "./SearchBar.vue";
export default {
  components: {
    SearchBar,
  },
  data() {
    return {
      api_key: "256cb5f777406806a05669637a427cda",
      url_base: "http://api.openweathermap.org/data/2.5/",
      weather: {},
      icon: "",
      description: "",
    };
  },
  props: {
    msg: String,
  },
  methods: {
    fetchData(data) {
      fetch(`${this.url_base}weather?q=${data}&appid=${this.api_key}`)
        .then((res) => {
          return res.json();
        })
        .then(this.setResults);
    },
    setResults(results) {
      this.weather = results;
      this.icon =
        "http://openweathermap.org/img/wn/" +
        this.weather.weather[0].icon +
        "@2x.png";
      this.description =
        this.weather.weather[0].description.charAt(0).toUpperCase() +
        this.weather.weather[0].description.slice(1);
    },
    dateBuilder() {
      let dates = new Date();
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
      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];

      let day = days[dates.getDay()];
      let date = dates.getDate();
      let month = months[dates.getMonth()];
      let year = dates.getFullYear();

      return `${day}, ${date} ${month} ${year}`;
    },
  },
};
</script>

<style></style>

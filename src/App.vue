<template>
  <Weather />
</template>

<script>
import Weather from "./components/Weather.vue";

export default {
  name: "App",
  components: {
    Weather
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Bree+Serif&display=swap");

#app {
  font-family: "Bree Serif", serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  /* background-image: url("https://picsum.photos/1700/800?random=1");
  filter: brightness(80%); */
}

</style>

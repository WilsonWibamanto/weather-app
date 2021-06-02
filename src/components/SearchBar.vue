<template>
  <div class="mx-auto w-5/6 md:w-1/2" @keyup.enter="enter">
    <input
      type="text"
      id="search"
      class="placeholder-black text-2xl text-black px-12 w-full h-20"
      placeholder="Enter a Location..."
      v-model="model"
      
    />
    <div class="float-right relative right-5 bottom-16 bg-black pb-1 px-3 w-max h-max rounded-full">
      <p><i class="fa fa-search" @click="press(model)"></i></p>
    </div>
  </div>
</template>

<script>
export default {
  emits: ["enter","press"],
  data() {
    return {
      model: ""
    };
  },
  methods: {
    enter(e) {
      this.$emit("enter", e.target.value);
    },
    press(data) {
      this.$emit("press", data);
    },
  },
};
</script>

<style scoped>
#search {
  -webkit-animation: random 30s infinite;
  animation: random 20s infinite;
  border-radius: 16px;
  transition: 0.5s;
  outline: none;
}
#search:focus {
  border-radius: 56px;
  animation-play-state: paused;
}
@keyframes random {
  10% {
    background-color: red;
  }
  30% {
    background-color: yellow;
  }
  45% {
    background-color: rgb(6, 255, 6);
  }
  60% {
    background-color: blue;
  }
  75% {
    background-color: white;
  }
}
</style>

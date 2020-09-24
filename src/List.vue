<template>
  <div id="app">
    <div>
      <Timer v-for="timer in timerCounter" :key="timer"/>
      <button v-on:click="addTimer()">+</button>
    </div>
  </div>
</template>

<script>
import Timer from '@/components/Timer.vue';

export default {
  data: () => ({
    timerCounter: 0,
  }),
  components: {
    Timer,
  },
  methods: {
    addTimer() {
      this.timerCounter += 1;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

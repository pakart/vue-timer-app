<template>
  <div id="inner-app">
    <div class="timers-container">
      <Timer v-for="timer in timerCounter" :key="timer"/>
      <div class="add-timer-block" v-on:click="addTimer()">
        <div class="plus-icon"></div>
      </div>
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

#inner-app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    display: flex;
    justify-content: center;
    margin-top: 100px;
    align-items: center;
    flex-direction: row;
    background-color: #353638;
    width: 300px;
}

@media (min-width: 768px) and (max-width: 1023px) {
  #inner-app {
    width: 600px;
  }
}
@media  (min-width:1024px) {
  #inner-app {
    width: 900px;
  }
}

.timers-container{
  height: auto;
  width: 100%;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  padding-left: 50px;
}

.add-timer-block{
  width: 225px;
  height: 120px;
  background-color: #696969;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  margin-right: 50px;
  margin-bottom: 25px;
}
.plus-icon{
  display:inline-block;
  width:40px;
  height:40px;
  background:
    linear-gradient(#9E9E9E,#9E9E9E),
    linear-gradient(#9E9E9E,#9E9E9E);
  background-position:center;
  background-size: 50% 3px,3px 50%;
  background-repeat:no-repeat;
}
</style>

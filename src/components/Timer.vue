<template>
  <div>
    <h1>{{resultTimeString}}</h1>
    <hr>
    <button v-on:click="startStopTimer()">start</button>
    <button v-on:click="dropTimer()">drop</button>
  </div>
</template>

<script>
export default {
  data: () => ({
    isActive: false,
    timerId: 0,
    seconds: 0,
    resultTimeString: '0',
  }),
  methods: {
    startStopTimer() {
      if (this.isActive === false) {
        console.log('start');
        this.isActive = true;
        // eslint-disable-next-line prefer-arrow-callback
        this.timerId = setInterval(function () {
          this.seconds += 1;
          this.resultTimeString = this.timeFormater(this.seconds);
        }.bind(this), 1000);
      } else {
        console.log('stop');
        clearTimeout(this.timerId);
        this.isActive = false;
      }
    },
    timeFormater(sec) {
      if (sec < 60) {
        return sec.toString();
      }
      if (sec < 3600) {
        return `${Math.trunc(sec / 60).toString()}:${(sec % 60).toString()}`;
      }
      return `${Math.trunc(sec / 3600).toString()}:${Math.trunc((sec % 3600) / 60).toString()}:${((sec % 3600) % 60).toString()}`;
    },
    dropTimer() {
      clearTimeout(this.timerId);
      this.seconds = 0;
      this.resultTimeString = '0';
      this.isActive = false;
      console.log('CLEARED');
    },
  },
};
</script>

<style>

</style>

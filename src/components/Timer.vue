<template>
  <div class="timer-body">
    <h3 class="string inactive" v-bind:class="{active: isActive}">{{resultTimeString}}</h3>
    <hr class="line inactive" v-bind:class="{active: isActive}">
    <div class="buttons-container">
      <div class="button play"
      v-bind:class="{pause: isActive}" v-on:click="startStopTimer()"></div>
      <div class="drop-button inactive"
      v-bind:class="{active: isActive}" v-on:click="dropTimer()"></div>
    </div>
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

  .string.inactive{
    color: #9E9E9E;
  }
  .string.active{
    color: #FFFFFF;
  }
  .line.inactive{
    height: 1px;
    color: #9E9E9E;
    border-width: 0;
    background-color: #9E9E9E;
  }
  .line.active{
    color: #FFFFFF;
    background-color: #FFFFFF;
  }
  .buttons-container{
    margin-top: 20px;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
  }
  .timer-body {
    width: 225px;
    height: 120px;
    background-color: #696969;
    margin-right: 50px;
    margin-bottom: 45px;
  }

  .button.play {
    margin-right: 50px;
    width: 20px;
    height: 20px;
    box-sizing: border-box;
    border-style: solid;
    border-width: 10px 0px 10px 20px;
    border-color: transparent transparent transparent #9E9E9E;
  }
  .button.pause {
    width: 20px;
    height: 20px;
    border-style: double;
    border-width: 0px 0px 0px 10px;
    border-color: #FFFFFF;
  }
  .drop-button.inactive {
    width: 20px;
    border-style: solid;
    border-width: 20px 0px 0px 0px;
    border-color:#9E9E9E;
  }
  .drop-button.active{
    border-color:#FFFFFF;
  }
</style>

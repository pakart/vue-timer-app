<!-- Компонент-секундомер с отображением времени, кнопками старт/пауза и сброса секундомера
с динамической сменой стилей -->
<template>
  <div class="timer-body">
    <!-- Элемент, отображаеющий текущее время секундомера -->
    <div class="string inactive" v-bind:class="{active: isActive}">{{resultTimeString}}</div>
    <!-- Элемент - горизонтальная линия -->
    <hr class="line inactive" v-bind:class="{active: isActive}">
    <!-- Элемент-контейнер для кнопок -->
    <div class="buttons-container">
      <!-- Кнопка старт-пауза -->
      <div class="button play"
      v-bind:class="{pause: isActive}" v-on:click="startStopTimer()"></div>
      <!-- Кнопка сброса -->
      <div class="drop-button inactive"
      v-bind:class="{active: isActive}" v-on:click="dropTimer()"></div>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    // флаг состояния активности
    isActive: false,
    // id таймера для управления
    timerId: 0,
    // количество секунд
    seconds: 0,
    // результирующая строка прошедшего времени
    resultTimeString: '0',
  }),
  methods: {
    // метод запуска/остановки секундомера
    startStopTimer() {
      // проверка состояния с последующим стартом/остановкой секундомера
      if (this.isActive === false) {
        this.isActive = true;
        // eslint-disable-next-line prefer-arrow-callback
        this.timerId = setInterval(function () {
          this.seconds += 1;
          this.resultTimeString = this.timeFormater(this.seconds);
        }.bind(this), 1000);
      } else {
        clearTimeout(this.timerId);
        this.isActive = false;
      }
    },
    // метод конвертирования прошедших секунд в необходимый кастомный формат отображения времени
    timeFormater(sec) {
      // прошло меньше минуты
      if (sec < 60) {
        return sec.toString();
      }
      // прошло меньше часа
      if (sec < 3600) {
        return `${Math.trunc(sec / 60).toString()}:${((sec % 60) < 10 ? `0${(sec % 60).toString()}` : (sec % 60).toString())}`;
      }
      // час+
      const mm = Math.trunc((sec % 3600) / 60).toString();
      const ss = ((sec % 3600) % 60).toString();
      return `${Math.trunc(sec / 3600).toString()}:${mm < 10 ? `0${mm}` : mm}:${ss < 10 ? `0${ss}` : ss}`;
    },
    // метод сброса секундомера
    dropTimer() {
      clearTimeout(this.timerId);
      this.seconds = 0;
      this.resultTimeString = '0';
      this.isActive = false;
    },
  },
};
</script>

<style>
  /* неактивное состояние строки времени */
  .string.inactive{
    font-size: 22px;
    font-weight: 400;
    margin-top: 18px;
    margin-bottom: 16px;
    color: #9E9E9E;
  }
  /* активное состояние строки времени */
  .string.active{
    color: #FFFFFF;
  }
   /* неактивное состояние полосы */
  .line.inactive{
    height: 1px;
    color: #9E9E9E;
    border-width: 0;
    background-color: #9E9E9E;
  }
  /* активное состояние полосы */
  .line.active{
    color: #FFFFFF;
    background-color: #FFFFFF;
  }
  /* стили контейнера кнопок */
  .buttons-container{
    margin-top: 20px;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
  }
  /* контейнер секундомера */
  .timer-body {
    width: 225px;
    height: 120px;
    background-color: #696969;
    margin-right: 50px;
    margin-bottom: 45px;
  }

  /* css иконка "play" */
  .button.play {
    margin-right: 50px;
    width: 20px;
    height: 20px;
    box-sizing: border-box;
    border-style: solid;
    border-width: 10px 0px 10px 20px;
    border-color: transparent transparent transparent #9E9E9E;
  }
  /* css иконка "pause" */
  .button.pause {
    width: 20px;
    height: 20px;
    border-style: double;
    border-width: 0px 0px 0px 10px;
    border-color: #FFFFFF;
  }
  /* неактивная css иконка "reset" */
  .drop-button.inactive {
    width: 20px;
    border-style: solid;
    border-width: 20px 0px 0px 0px;
    border-color:#9E9E9E;
  }
  /* активная css иконка "reset" */
  .drop-button.active{
    border-color:#FFFFFF;
  }
</style>

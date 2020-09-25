<!-- Компонент-список для отображения секундомеров -->
<template>
  <div id="inner-app">
    <div class="timers-container">
      <!-- Рендер необходимого количества компонентов-секундомеров -->
      <Timer v-for="timer in timerCounter" :key="timer"/>
      <!-- Кнопка добавления нового компонента-секундомера -->
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
    // Счётчик количества секундомеров
    timerCounter: 0,
  }),
  components: {
    Timer,
  },
  methods: {
    // Метод обновления счётчика
    addTimer() {
      this.timerCounter += 1;
    },
  },
};
</script>

<style>
  /* Стили для корректного отображения адаптива внутреннего контейнера */
  #inner-app {
      font-family: Gotham Pro, Avenir, Helvetica, Arial, sans-serif;
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
  /* Контейнер секундомеров */
  .timers-container{
    height: auto;
    width: 100%;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    padding-left: 50px;
  }
  /* Кнопка добавления таймера */
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
  /* css иконка плюса */
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

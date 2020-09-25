<template>
  <div id="app">
    <List />
  </div>
</template>

<script>
import List from '@/List.vue';

export default {
  name: 'App',
  components: {
    List,
  },
};
</script>

<style>
html{
  height: 100%;
}
body{
  height: 100%;
  margin: 0;
  background-color: #353638;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #353638;
}
</style>

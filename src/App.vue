<template>
  <v-app>
    <h1 align:center><b>COVID 19 TRACKER</b></h1>
    <hr>
    <Tracker />
  </v-app>
</template>

<script>
import Tracker from './components/Tracker.vue';

export default {
  name: 'App',

  components: {
    Tracker
  }
};
</script>

<style scoped>
h1{
  position: relative;
  width: 100%;
  align-self: center;
  text-align: center;
  font-family: 'archia';
}
</style>
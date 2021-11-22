<template>
  <HeaderApp title="Store Resource"></HeaderApp>
  <resources/>
</template>

<script>
import HeaderApp from "./components/Header/HeaderApp.vue";
import Resources from './components/Resources/Resources.vue';


export default {
  name: 'App',
  components: {HeaderApp, Resources}
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');
* {
  box-sizing: border-box;
}
html {
  font-family: 'Roboto', sans-serif;
}
body {
  margin: 0;
}
</style>
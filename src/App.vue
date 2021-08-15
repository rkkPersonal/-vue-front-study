<template>
  <div id="app">
    <!-- <router-view />
    <my-component></my-component>
    <register-component></register-component> -->
    <home-page></home-page>
  </div>

</template>

<script>
import HomePage from './components/HomePage.vue';
export default {
  components: { HomePage },
  name: "App"
};
</script>

<style></style>

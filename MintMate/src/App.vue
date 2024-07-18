<template>
  <Suspense>
    <template #default>
      <Home></Home>
    </template>
    <template #fallback>
      <splashscreen></splashscreen>
    </template>
  </Suspense>
</template>

<script >
  import splashscreen from './components/SplashScreen.vue';
  import { defineAsyncComponent } from 'vue';
  export default {
    components: {
      splashscreen,
      Home: defineAsyncComponent(() => {
      return new Promise((resolve) => {
        setTimeout(() => {
          resolve(import("./components/Home.vue"));
        }, 2500);
      });
    })
        }
  }
</script>


<style>
  html,
  body,
  .app {
    min-height: 100vh;
    margin: 0;
    font-family: Arial, Helvetica, sans-serif;
  }
  * {
    --brand-green: #04b500;
    --brand-blue: #0689b0;
  }
</style>

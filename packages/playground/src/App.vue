<script setup>
import { RouterView } from 'vue-router';
import HelloWorld from './components/HelloWorld.vue';
</script>

<template>
  <header>
    <img src="@/assets/logo.svg" width="60" height="60" />
    <div class="wrapper">
      <HelloWorld msg="VTV Starter" />
    </div>
  </header>
  <RouterView />
</template>

<style scoped>
header {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>

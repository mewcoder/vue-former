<script setup>
import demo from '../mock/demo.json';

const json = demo;

const prefix = 'el';
</script>

<template>
  <div class="home">
    <VFormer :schema="json" prefix="El" />
  </div>
</template>

<style>
.home {
  width: 500px;
  margin: auto;
  border: 1px solid silver;
  padding: 20px;
}
</style>

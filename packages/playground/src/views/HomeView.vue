<script setup>
import demo from '../mock/demo.json';

const json = demo;

const prefix = 'El';
</script>

<template>
  <div class="home">
    <pre class="pre">{{ JSON.stringify(json, null, 2) }}</pre>
    <VFormer class="form" :schema="json" :prefix="prefix" />
  </div>
</template>

<style scoped>
.home {
  margin: auto;
  display: flex;
  width: 800px;
}
.pre {
  width: 400px;
}

.form {
  width: 400px;
  border: 1px solid silver;
  padding: 20px;
}
</style>

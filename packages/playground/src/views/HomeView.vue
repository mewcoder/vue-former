<script setup>
import { ref } from 'vue';
import demo from '../mock/demo.json';

const json = demo;

const prefix = 'El';

const formRef = ref();

function getForm() {
  const data = formRef.value.getForm();
  alert(JSON.stringify(data, null, 2));
}
function resetForm() {
  formRef.value.resetFields();
}
</script>

<template>
  <div class="home">
    <pre class="pre">{{ JSON.stringify(json, null, 2) }}</pre>
    <div>
      <VFormer ref="formRef" class="form" :schema="json" :prefix="prefix" />
      <el-button type="primary" @click="getForm()">Submit</el-button>
      <el-button @click="resetForm()">Reset</el-button>
    </div>
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

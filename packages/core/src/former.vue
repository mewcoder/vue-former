<script setup>
import { ref, computed, reactive, watch } from 'vue';
import FormerItem from './former-item.vue';
import { cloneDeep } from 'lodash-es';

const props = defineProps({
  schema: {
    type: Array,
    default: () => []
  },
  config: {
    type: Object,
    default: () => ({ labelPosition: 'top' })
  },
  rules: {
    type: Object,
    default: () => ({})
  },
  prefix: {
    type: String,
    default: 'el'
  }
});

const formRef = ref();

const formKey = props.prefix + '-form';
const formItemKey = props.prefix + '-form-item';

const renderList = computed(() => {
  return props.schema;
});

const formData = reactive({});

const formRule = reactive({});

watch(
  () => props.schema,
  (val) => {
    if (!val || !val.length) return;
    const list = cloneDeep(val);
    initFormData(list);
    initFormRules(list);
  },
  { deep: true, immediate: true }
);

function initFormData(list) {
  const data = {};
  for (const item of list) {
    initItemValue(item, data);
  }
}

function initItemValue(item) {
  const { model, value } = item;
  formData[model] = value;
}

function initFormRules() {
  for (const key in props.rules) {
    formRule[key] = props.rules[key];
  }
}

//-----------------------------API-----------------------------
function getForm() {
  // 获取页面操作的字段信息
  const form = cloneDeep(formData);
  return form;
}

function resetFields() {
  formRef.value.resetFields();
}

defineExpose({ getForm, resetFields });
</script>

<template>
  <!-- <form> -->
  <component
    ref="formRef"
    :is="formKey"
    :model="formData"
    :rules="formRule"
    v-bind="config"
    @submit.prevent
  >
    <template v-for="(item, i) in renderList" :key="item.model + i">
      <!-- <form-item> -->
      <component
        :is="formItemKey"
        :prop="item.model"
        :label="item.label || ''"
        :description="item.description || ''"
        v-bind="item.config || {}"
      >
        <!-- component -->
        <component
          :is="item.type"
          :key="item.model + item.type"
          :ref="'filed-' + item.model"
          v-model="formData[item.model]"
          v-bind="item.props"
        >
          <!-- slots -->
          <template v-for="slot in item.slots" :key="slot.name" #[slot.name]>
            <FormerItem
              v-if="slot.children"
              :key="slot.name"
              :schema="slot.children"
            />
          </template>
          <!-- children -->
          <FormerItem v-if="item.children" :schema="item.children" />
        </component>
      </component>
    </template>
  </component>
</template>

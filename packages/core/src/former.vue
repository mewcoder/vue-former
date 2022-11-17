<script setup>
import { computed, reactive } from 'vue';
import FormerItem from './former-item.vue';

const props = defineProps({
  schema: {
    type: Array,
    default: () => []
  },
  prefix: {
    type: String,
    default: 'el'
  }
});

const formKey = props.prefix + '-form';
const formItemKey = props.prefix + '-form-item';

const renderList = computed(() => {
  return props.schema;
});

const formData = reactive({});
</script>

<template>
  <!-- <form> -->
  <component :is="formKey" :modal="formData" @submit.prevent>
    <!-- <form-item> -->
    <component
      :is="formItemKey"
      v-for="item in renderList"
      :key="item.model"
      :prop="item.model"
      :label="item.label || '--'"
      :description="item.description || '--'"
    >
      <!-- content -->
      <component
        :is="item.type"
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
  </component>
  <pre>{{ JSON.stringify(schema, null, 2) }}</pre>
</template>

<script setup>
const props = defineProps({
  schema: {
    type: Array,
    default: () => []
  }
});

console.log(props.schema);
</script>

<template>
  <span>
    <template v-for="(child, index) in schema">
      <component
        v-if="typeof child === 'object'"
        :is="child.type"
        :key="index"
        v-bind="child.props"
      >
        <FormerItem v-if="child.children" :schema="child.children" />
      </component>
      <template v-else>
        {{ child }}
      </template>
    </template>
  </span>
</template>

<script>
export default {
  name: 'FormerItem'
};
</script>

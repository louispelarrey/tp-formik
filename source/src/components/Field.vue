<script setup>
import { computed, defineProps, ref } from "vue";

const props = defineProps({
  as: {
    type: String,
    default: "text",
  },
  name: {
    type: String,
    required: true,
  },
});

const type = ref("");
const component = computed(() => {
  if (props.as === "textarea") {
    return "textarea";
  }
  if (props.as === "select") {
    type.value = null;
    return "select";
  }
  if (props.as === "number") {
    type.value = "number";
    return "input";
  }
  return "input";
});

const handleChange = (e) => {
  addFormField(props.name, e.target.value);
};
</script>

<template>
  <component :is="component" @input="handleChange" :type="type">
    <slot v-if="as === 'select'"></slot>
  </component>
</template>

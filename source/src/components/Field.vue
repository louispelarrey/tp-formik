<script setup>
import { computed, defineProps, reactive, ref, inject } from "vue";
import { setValueChange, valuesKey } from "./FormixProvider";

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
const values = inject(valuesKey);
</script>

<template>
  <component :is="as" :type="type" :name="name" :value="values[name]" @input="e => values[name] = e.target.value">
    <slot></slot>
  </component>
</template>

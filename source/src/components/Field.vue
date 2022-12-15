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
  for (let i = 0; i < props.as.length; i++) {
    if (props.as[i] === props.as[i].toUpperCase()) {
      type.value = props.as.slice(i).toLowerCase();
      return props.as.slice(0, i);
    }
  }
  return props.as;
});

const values = inject(valuesKey);
</script>

<template>
  <component :is="as" :type="type" :name="name" :value="values[name]" @input="e => values[name] = e.target.value">
    <slot></slot>
  </component>
</template>

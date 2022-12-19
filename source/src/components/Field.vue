<script setup>
import { defineProps, ref, inject } from "vue";
import { valuesKey } from "./FormixProvider";

const props = defineProps({
  as: {
    type: String,
  },
  name: {
    type: String,
  },
});

const type = ref("");
const values = inject(valuesKey);
</script>

<template>
  <component :is="as || 'input'" :type="type" :name="name" :value="values[name]"
    @input="(e) => (values[name] = e.target.value)">
    <slot></slot>
  </component>
</template>

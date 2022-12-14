<script setup>
import {reactive, provide } from "vue";
import { valuesKey, setValueChange } from "./FormixProvider";

const props = defineProps({
  initialValues: {
    type: Object,
    required: true,
  },
  validate: {
    type: Function,
    required: false,
  },
  onSubmit: {
    type: Event,
    default: () => {},
  },
})

const values = reactive(props.initialValues);
provide(valuesKey, values);

function handleChange(event) {
  console.log("Handle change trigger", event.target.value);
  values.value = event.target.value;
  setValueChange(props.name, event.target.value);
}

function handleSubmit(event) {
  event.preventDefault();
  props.onSubmit(values);
}


</script>

<template>
  <p>{{ JSON.stringify(values) }}</p>
    <slot 
      :values="values" 
      :handleChange="handleChange"
      :handleSubmit="handleSubmit"
    ></slot>
  
</template>
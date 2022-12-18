<script setup>
import { reactive, provide, ref } from "vue";
import { valuesKey } from "./FormixProvider";

const { initialValues, validate, onSubmit } = defineProps({
  initialValues: {
    type: Object,
    required: true,
  },
  validate: {
    type: Function
  },
  onSubmit: {
    type: Function,
  },

})

const errors = ref([]);
const isSubmitted = ref(false);
const values = reactive(initialValues);

provide(valuesKey, values);

function handleSubmit() {
  console.log("Formix.vue Submit", values); 
  isSubmitted.value = false;

  errors.value = validate(values);
  if (errors.value.length === 0) {
    onSubmit(values);
    isSubmitted.value = true;
  }
}
</script>

<template>
  <p>{{ JSON.stringify(values) }}</p>
  <form @submit.prevent="handleSubmit">
    <p v-if="errors.length > 0">Errors: </p>
    <ul>
      <li v-for="error in errors">
        {{ error.level }}
      </li>
    </ul>
    <slot></slot>
  </form>
  <p v-if="isSubmitted">
    Form submitted
  </p>
</template>
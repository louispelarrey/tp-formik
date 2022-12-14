<script setup>
import {reactive} from "vue";

const formData = reactive({})

const addFormField = (name, value) => {
  formData[name] = value
}

</script>

<template>
  <p>{{ JSON.stringify(formData) }}</p>
  <slot :addFormField="addFormField"></slot>
</template>
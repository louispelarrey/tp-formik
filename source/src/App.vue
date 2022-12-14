<script setup>
import Formix from './components/Formix.vue';
import Field from './components/Field.vue';
</script>

<template>
   <Formix v-slot="{addFormField}">
    <Field name="level" as="select">
      <option>1</option>
      <option>2</option>
      <option>3</option>
    </Field>
    <Field name="username" as="text" />
    <Field name="bio" as="textarea"/>
    <button @click="() => addFormField('zob', '19cm')">Click salope</button>
  </Formix>
</template>

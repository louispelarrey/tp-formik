<script setup>
import Formix from './components/Formix.vue';
import Field from './components/Field.vue';

import * as yup from 'yup';
import { reactive } from 'vue';

const initialValues = reactive({
  level: 0,
  username: "azekjha",
  bio: "qsdkjnsd"
});

let validateSchema = yup.object({
  level: yup.number().required(),
  username: yup.string().required(),
  bio: yup.string().required()
});

const onSubmit = (values) => {
  console.log(values);
}
</script>

<template>
   <Formix
    :initialValues="initialValues"
    :validate="validateSchema.validate"
    @onsubmit="onSubmit"
    >
    <Field name="level" as="select">
      <option>1</option>
      <option>2</option>
      <option>3</option>
    </Field>
    <Field name="username" as="text" />
    <Field name="bio" as="textarea"/>
    <button @click="onSubmit">Submit</button>
  </Formix>
</template>

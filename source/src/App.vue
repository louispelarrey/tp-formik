<script setup>
import Formix from './components/Formix.vue';
import Field from './components/Field.vue';
import { setValueChange, valuesKey } from "./components/FormixProvider";

import * as yup from 'yup';
import { reactive, inject, provide } from 'vue';

const initialValues = reactive({
  level: 0,
  age: 2,
  bio: "Default Bio",
  birth: "2021-01-01"
});

let validateSchema = yup.object({
  level: yup.number().required(),
  username: yup.string().required(),
  bio: yup.string().required()
});

const validate = (values) => {
  const errors = [];
  if (!values["level"]) {
    errors.push({level: "Level field is required"})
  }
  if (values["bio"].length < 5) {
    errors.push({level: "Bio field must be at least 5 characters long"})
  }
  return errors;
};

const handleSubmit = (values) => {
  console.log("App.vue Submit", values);
}
</script>

<template>
  <Formix :initialValues="initialValues" :validate="validate" :onSubmit="handleSubmit">
      <Field name="level" as="select">
        <option>1</option>
        <option>2</option>
        <option>3</option>
      </Field>
      <Field name="bio" as="textarea" />
      <Field name="age" type="number" />
      <Field name="birth" type="date" />
      <Field as="button" @click="onSubmit">Submit</Field>
  </Formix>
</template>

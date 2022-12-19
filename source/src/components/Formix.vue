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
  <form @submit.prevent="handleSubmit">
    <slot></slot>
    <div v-if="errors.length > 0" class="submitError">
      Errors:
      <ul>
        <li v-for="error in errors">
          {{ error.level }}
        </li>
      </ul>
    </div>
    <div v-if="isSubmitted" class="submitSuccess">
        Success : Form is submitted
    </div>

    
  </form>

  <div>
    <!--Afficher ces informations 1 par 1 <p>{{ JSON.stringify(values) }}</p>-->
    <div class="infosElement"> 
      <p>Live informations :</p>
      <p>Level : {{ values.level }}</p>
      <p>Bio : {{ values.bio }}</p>
    </div>
  </div>
  

</template>
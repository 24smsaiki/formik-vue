<script setup>
import { ref, reactive, provide } from 'vue'
import Formik from './components/Formik.vue';
import Field from './components/Field.vue';

const onSubmit = (values) => {
  
    for (let key in values) {
        if (values.hasOwnProperty(key)) {
            values[key] = '';
          }
    }
};

const validate = (values) => {
    const errors = {}
    if (!values.name) {
        errors.name = 'Required'
    } else if (values.name.length > 15) {
        errors.name = 'Must be 15 characters or less'
    }
    if (!values.email) {
        errors.email = 'Required'
    } else if (!/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}$/i.test(values.email)) {
        errors.email = 'Invalid email address'
    }
    return errors
}

const initialValue = reactive({
    name: '',
    email: '',
    select: [
       "toto", "tata", "titi"
    ],
});

</script>

<template>
  <header>
    <div class="wrapper">
      <Formik
        :initialValues="initialValue"
        :onSubmit="onSubmit"
        :validate="validate"
      >
        <template #default="{ values, errors, handleSubmit, isSubmitting }">
          <form @submit.prevent="handleSubmit">
            <Field
              as="input"
              name="name"
              v-model:value="values.name"
              />
              <Field
                as="input"
                name="email"
                placeholder="email"
              />

            <Field
              as="select"
              name="select"
            >
              <option v-for="option in values.select" :value="option" :key="option">
                {{ option }}
              </option>
            </Field>

            
            <button type="submit" :disabled="isSubmitting">Submit</button>

          <div v-if="errors" >
            <div v-for="(error, key) in errors" :key="key">
              {{ error }}
            </div>
          </div>
          </form>
        </template>
      </Formik>

    </div>
  </header>


</template>

<style scoped>
</style>

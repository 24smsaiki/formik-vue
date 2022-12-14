<script setup>
import { ref, reactive, provide } from 'vue';

const props = defineProps({
   initialValues: {
      type: Object,
      required: true
   },
    onSubmit: {
        type: Function,
        required: true
    },
    validate: {
        type: Function,
        required: true
    }
});

const values = ref(props.initialValues);

const handleSubmit = (e) => {
    e.preventDefault()
    const formValues = values.value;
    const formErrors = props.validate(formValues);
    if (Object.keys(formErrors).length === 0) {
        props.onSubmit(formValues);
    } else {
        errors.value = formErrors;
    }
    console.log(formValues);
}

const isSubmitting = ref(false);
const errors = reactive({});

provide('values', values);
</script>

<template>
     <slot :values="values" :errors="errors" :handleSubmit="handleSubmit" :isSubmitting="isSubmitting"></slot>
</template>
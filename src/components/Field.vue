<script setup>
import { ref, reactive, inject } from 'vue'

const props = defineProps({
    as: {
        type: String,
        required: true,
        default: 'input'
    },
    name: {
        type: String,
        required: true
    },
})

const values = inject('values');


</script>



<template>
    <keep-alive>
        <component :is="as" v-if="(typeof props.as === 'string')" @input="values[props.name] = $event.target.value">
            
            <slot></slot>
        </component>
        <component :is="as" v-else v-model="values[props.name]">
            <slot></slot>
        </component>
    </keep-alive>
</template>
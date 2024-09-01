<template>
            <v-select
              :model-value="modelValue"
              @update:modelValue="updateValue"
              label="Select"
              :items="['Teacher', 'Student']"
            ></v-select>
  </template>
  
  <script lang="ts">
  import { defineComponent, ref } from 'vue';
  
  export default defineComponent({
    name: 'Permission_practice',
    props: {
      modelValue: {
        type: String,
        required: true
      }
    },
    methods: {
      updateValue(value: string) {
        this.$emit('update:modelValue', value);
      },
    }
  });
  </script>

<template>
    <button :class="['custom-button', `button-${type}`]">{{ text }}</button>
  </template>
  
  <script setup>
  import { defineProps } from 'vue';
  
  const props = defineProps({
    text: {
      type: String,
      default: 'Exemplo'
    },
    type: {
      type: String,
      default: 'default',
      validator: (value) => ['default', 'cancel', 'warning'].includes(value)
    }
  });
  </script>
  
  <style scoped>
  .custom-button {
    width: 100%;
    height: fit-content;
    padding: 0.5em;
    border-radius: 0.5em;
    border: none;
    box-shadow: 0 0.25em 1em rgba(0, 0, 0, 0.3);
    transition: all 0.2s ease-in-out;
    background-color: transparent;
    font-size: 1em;
  }
  
  .button-default {
    background-color: white;
    border: 2px solid var(--default);
    color: var(--default);
  }
  
  .button-default:hover {
    background-color: var(--default);
    color: white;
  }
  
  .button-cancel {
    background-color: white;
    border: 2px solid var(--cancel);
    color: var(--cancel);
  }
  
  .button-cancel:hover {
    background-color: var(--cancel);
    color: white;
  }
  
  .button-warning {
    background-color: white;
    border: 2px solid var(--warning);
    color: var(--warning);
  }
  
  .button-warning:hover {
    background-color: var(--warning);
    color: white;
  }
  </style>
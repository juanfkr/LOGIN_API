<template>
  <div class="header">
    <ButtonComponent @click="formTarget = 'login'" type="default" text="Login"/>
    <ButtonComponent @click="formTarget = 'register'" type="default" text="Registro"/>
  </div>
  <div>
    <Login v-if="formTarget === 'login'" />
    <Register v-if="formTarget === 'register'" />
  </div>
</template>

<script setup>
import ButtonComponent from '@/components/ui/ButtonComponent.vue';
import Register from '@/components/ui/Register.vue';
import Login from '@/components/ui/Login.vue';
import { ref } from 'vue';

const formTarget = ref('login')
</script>

<style scoped>
.header {
  display: flex;
  gap: .5em;
  min-width: 400px;
  max-width: 100px;
}
</style>

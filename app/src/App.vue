<script setup lang="ts">
import { ref } from 'vue';

const name = ref('John Doe');
const status='active';


</script>

<template>
  <!-- <h1>Vue Jobs</h1> -->
  <h1>{{ name }}</h1>
  <p v-if="status=='active'">Vue 3 is awesome</p>
  <p v-else-if="status=='inactive'">Vue 3 is not awesome</p>
  <p v-else>Vue 3 is not awesome</p>
</template>



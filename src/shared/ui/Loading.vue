<script setup lang="ts">
import { ref } from 'vue';

defineProps<{ show: boolean }>();
</script>

<template>
  <div v-show="show" class="text-center text-secondary">
    <div class="spinner-border m-5" role="status"></div>
  </div>
</template>

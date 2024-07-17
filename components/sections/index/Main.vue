<template>
  <div class="main cut-section">
  </div>
</template>
<script setup lang="ts">
const authStore = useAuthStore();
const { isAuthenticated } = storeToRefs(authStore);
</script>

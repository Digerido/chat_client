<template>
  <div class="m-page admin-page">
    <div
      v-if="commonStore.categories"
      class="wrapper"
      :class="{ wrapper__full: full }"
    >
      <SectionsCommonHeaderProfile :user="userStore.user" />
      <main class="content" :class="{ content__chat: full }">
        <slot></slot>
      </main>
      <SectionsCommonFooterProfile />
    </div>
  </div>
</template>

<script setup lang="ts">
definePageMeta({
  middleware: "authenticated",
});
const userStore = useUserStore();
const commonStore = useCommonStore();
const full = computed(() => {
  return useRoute().path.includes("/messages");
});
</script>

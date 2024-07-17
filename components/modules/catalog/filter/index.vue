<template>
</template>

<script setup lang="ts">
import type { CatalogStores } from "~/stores/catalog/catalog.type";
const show = defineModel<boolean>("show", { required: true });
watch(show, (value) => {
  if (value) {
    document.body.classList.add("open-filter");
    document.body.classList.add("fixed-body");
  } else {
    document.body.classList.remove("open-filter");
    document.body.classList.remove("fixed-body");
  }
});
const props = defineProps({
  store: {
    type: Object as PropType<CatalogStores>,
    required: true,
  },
});
const store = props.store;
const chooseUser = ref<string>();
const updateUser = async () => {
  const { data } = await apiFetch<ApiResponse<string>>(
    `/api/users/username/${props.store.filters.createdBy}`,
  );
  if (data.value) {
    chooseUser.value = data.value.result;
  }
};

watch(
  () => props.store.filters.createdBy,
  () => {
    if (props.store.filters.createdBy) {
      updateUser();
    }
  },
  { immediate: true },
);
</script>

<template>
  <div>
    <UIVBreadcrumbs
      :items="[{ name: 'Главная', to: '/' }, { name: 'Каталог проектов' }]"
    />
    <UIPageTop
      v-model="bufSearch"
      title="Поиск проектов"
      description="Вам доступно более 500 000 предложений"
      :has-search="true"
      @submit="setSearch()"
    />
    <ModulesCatalog :store="catalogStore">
      <template #items>
        <div v-if="catalogStore.items?.length" class="services-items">
          <ModulesCardsProject
            v-for="(el, index) in catalogStore.items"
            :key="catalogStore.items[index]._id"
            v-model="catalogStore.items[index]"
          />
        </div>

        <div
          v-else-if="
            !catalogStore.empty ||
            (!catalogStore.empty && !catalogStore.items?.length)
          "
          class="services-items"
        >
          <ModulesCardsProject v-for="i in 10" :key="i" />
        </div>
      </template>
      <template v-if="catalogStore.totalItems" #count>
        {{
          pluralize(catalogStore.totalItems, "проект", "проекта", "проектов")
        }}</template
      >
    </ModulesCatalog>
  </div>
</template>

<script setup lang="ts">
import { useCatalogProjectsStore } from "~/stores/catalog/projects";
const bufSearch = ref("");
const catalogStore = useCatalogProjectsStore();
const setSearch = () => {
  catalogStore.searchQuery = bufSearch.value;
};
useHead({
  title: "Каталог проектов",
});
</script>

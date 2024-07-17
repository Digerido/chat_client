<template>
  <div class="header-bottom">
  </div>
</template>

<script setup lang="ts">
import { useCommonStore } from "~/stores/common";
const commonStore = useCommonStore();

const list = ref([
  { title: "Разработка и ИТ", isHaveSubmenu: false },
  { title: "Дизайн и творчество", isHaveSubmenu: false },
  { title: "Цифровой маркетинг", isHaveSubmenu: false },
  { title: "Копирайтинг и перевод", isHaveSubmenu: false },
  { title: "Музыка и аудио", isHaveSubmenu: false },
  { title: "Видео и анимация", isHaveSubmenu: false },
  { title: "Копирайтинг и перевод", isHaveSubmenu: false },
  { title: "Еще", isHaveSubmenu: true },
]);
</script>

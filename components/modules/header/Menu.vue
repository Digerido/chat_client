<template>
  <div class="master-menu">
    <button class="master-menu__toggle">
      <svg
        width="16"
        height="16"
        viewBox="0 0 16 16"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M14.125 8.625H10.5C9.46613 8.625 8.625 9.46613 8.625 10.5V14.125C8.625 15.1589 9.46613 16 10.5 16H14.125C15.1589 16 16 15.1589 16 14.125V10.5C16 9.46613 15.1589 8.625 14.125 8.625ZM14.75 14.125C14.75 14.4696 14.4696 14.75 14.125 14.75H10.5C10.1554 14.75 9.875 14.4696 9.875 14.125V10.5C9.875 10.1554 10.1554 9.875 10.5 9.875H14.125C14.4696 9.875 14.75 10.1554 14.75 10.5V14.125ZM5.5 8.625H1.875C0.841125 8.625 0 9.46613 0 10.5V14.125C0 15.1589 0.841125 16 1.875 16H5.5C6.53387 16 7.375 15.1589 7.375 14.125V10.5C7.375 9.46613 6.53387 8.625 5.5 8.625ZM6.125 14.125C6.125 14.4696 5.84462 14.75 5.5 14.75H1.875C1.53038 14.75 1.25 14.4696 1.25 14.125V10.5C1.25 10.1554 1.53038 9.875 1.875 9.875H5.5C5.84462 9.875 6.125 10.1554 6.125 10.5V14.125ZM5.5 0H1.875C0.841125 0 0 0.841125 0 1.875V5.5C0 6.53387 0.841125 7.375 1.875 7.375H5.5C6.53387 7.375 7.375 6.53387 7.375 5.5V1.875C7.375 0.841125 6.53387 0 5.5 0ZM6.125 5.5C6.125 5.84462 5.84462 6.125 5.5 6.125H1.875C1.53038 6.125 1.25 5.84462 1.25 5.5V1.875C1.25 1.53038 1.53038 1.25 1.875 1.25H5.5C5.84462 1.25 6.125 1.53038 6.125 1.875V5.5ZM14.125 0H10.5C9.46613 0 8.625 0.841125 8.625 1.875V5.5C8.625 6.53387 9.46613 7.375 10.5 7.375H14.125C15.1589 7.375 16 6.53387 16 5.5V1.875C16 0.841125 15.1589 0 14.125 0ZM14.75 5.5C14.75 5.84462 14.4696 6.125 14.125 6.125H10.5C10.1554 6.125 9.875 5.84462 9.875 5.5V1.875C9.875 1.53038 10.1554 1.25 10.5 1.25H14.125C14.4696 1.25 14.75 1.53038 14.75 1.875V5.5Z"
          fill="#222222"
        />
      </svg>
      <span>Категории</span>
    </button>

    <ul class="menu">
      <li
        v-for="category of commonStore.categories?.slice(0, 8)"
        :key="category._id"
      >
        <nuxtLink :to="`/services/${category.slug}`" class="menu__dropdown">
          <NuxtImg
            :src="baseUrl() + category.icon"
            crossorigin="anonymous"
            class="menu__icon"
            alt=""
          />
          <span class="menu__title">{{ category.title }}</span>
        </nuxtLink>
        <div v-if="category.sub?.length" class="drop-menu">
          <div class="drop-menu__grid">
            <div v-for="sub of category.sub" :key="sub" class="submenu">
              <div class="submenu__title text15 medium-text">UI/UX дизайн</div>
              <ul class="submenu__list">
                <li><a href="">Дизайн сайта</a></li>
                <li><a href="">Дизайн приложения</a></li>
                <li><a href="">UX-дизайн</a></li>
                <li><a href="">Дизайн целевой страницы</a></li>
                <li><a href="">Дизайн Иконок</a></li>
              </ul>
            </div>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
const commonStore = useCommonStore();

const list = ref([
  {
    title: "Разработка и ИТ",
    path: "menu-icon.svg",
  },
  {
    title: "Дизайн и творчество",
    path: "menu-icon2.svg",
  },
  {
    title: "Цифровой маркетинг",
    path: "menu-icon3.svg",
  },
  {
    title: "Копирайтинг и перевод",
    path: "menu-icon4.svg",
  },
  {
    title: "Музыка и аудио",
    path: "menu-icon5.svg",
  },
  {
    title: "Видео и анимация",
    path: "menu-icon6.svg",
  },
  {
    title: "Инженерия и архитектура",
    path: "menu-icon7.svg",
  },
  {
    title: "Финансы и бухгалтерский учет",
    path: "menu-icon8.svg",
  },
]);
</script>

<template>
  <div class="categories m-section">
    <div class="container">
      <UISectionTop
        title="Поиск исполнителя по специальности"
        desc="Получите вдохновение от более чем 1800 навыков"
        :link="{ text: 'Все категории', path: '/services/all' }"
      />

      <Swiper
        v-if="categories"
        class="categories-slider slider"
        :slides-per-view="'auto'"
      >
        <SwiperSlide v-for="card in categories.slice(0, 8)" :key="card._id">
          <NuxtLink :to="`/services/${card.slug}`" class="category-card">
            <div class="category-card__icon">
              <NuxtImg
                :src="baseUrl() + card.icon"
                crossorigin="anonymous"
                alt=""
              />
            </div>
            <div class="category-card__count">
              <span class="text15">{{
                pluralize(
                  card.services_count,
                  "предложение",
                  "предложения",
                  "предложений",
                )
              }}</span>
            </div>
            <div class="category-card__info">
              <div class="text20">{{ card.title }}</div>
              <div class="text14 light-text gray-text">
                Инженер-программист, веб-/мобильный разработчик и многое другое
              </div>
            </div>
          </NuxtLink>
        </SwiperSlide>
        <div class="swiper-nav">
          <div class="swiper-button swiper-button-prev">
            <svg
              width="24"
              height="24"
              viewBox="0 0 24 24"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M9.56995 18.0699L3.49995 11.9999L9.56995 5.92995"
                stroke="#5E67FF"
                stroke-width="1.5"
                stroke-miterlimit="10"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
              <path
                d="M20.5 12L3.67 12"
                stroke="#5E67FF"
                stroke-width="1.5"
                stroke-miterlimit="10"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
            </svg>
          </div>
          <div class="swiper-pagination"></div>
          <div class="swiper-button swiper-button-next">
            <svg
              width="24"
              height="24"
              viewBox="0 0 24 24"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M14.4301 5.93005L20.5001 12.0001L14.4301 18.0701"
                stroke="#5E67FF"
                stroke-width="1.5"
                stroke-miterlimit="10"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
              <path
                d="M3.5 12H20.33"
                stroke="#5E67FF"
                stroke-width="1.5"
                stroke-miterlimit="10"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
            </svg>
          </div>
        </div>
      </Swiper>
    </div>
  </div>
</template>

<script setup lang="ts">
const { categories } = storeToRefs(useCommonStore());
// const cardList = ref([
//   {
//     icon: 'category-icon.svg',
//     title: 'Разработка и ИТ',
//     slug: 'development',
//   },
//   {
//     icon: 'category-icon2.svg',
//     title: 'Дизайн и творчество',
//     slug: 'design',
//   },
//   {
//     icon: 'category-icon3.svg',
//     title: 'Цифровой маркетинг',
//     slug: 'marketing',
//   },
//   {
//     icon: 'category-icon4.svg',
//     title: 'Копирайтинг и перевод',
//     slug: 'all',
//   },
//   {
//     icon: 'category-icon5.svg',
//     title: 'Музыка и аудио',
//     slug: 'all',
//   },
//   {
//     icon: 'category-icon6.svg',
//     title: 'Видео и анимация',
//     slug: 'all',
//   },
//   {
//     icon: 'category-icon7.svg',
//     title: 'Инженерия и архитектура',
//     slug: 'all',
//   },
//   {
//     icon: 'category-icon8.svg',
//     title: 'Финансы и бухгалтерский учет',
//     slug: 'finances',
//   },
// ]);
</script>

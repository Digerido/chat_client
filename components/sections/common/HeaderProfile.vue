<template>
  <header class="admin-header">
    <div class="container">
      <div class="admin-header__inner">
        <nuxtLink to="/" class="admin-header__logo">
          <NuxtImg :preload="true" alt="Logo" />
        </nuxtLink>
        <ModulesHeaderAuth profile />
      </div>
    </div>
    <div class="admin-menu">
      <div class="mob-menu__account-top">
        <div class="text14 light-text gray-text">Навигация</div>
      </div>
      <ul class="mob-menu__links">
        <li v-for="item of links" :key="item.path">
          <NuxtLink
            :to="item.path"
            class="mob-menu__link"
            :active-class="'_active'"
          >
            <div v-html="item.icon" />
            <span class="mob-menu__title">{{ item.title }}</span>
            <div
              v-if="
                item?.key === 'messages' &&
                messagesStore?.totalUnseenMessages > 0
              "
              class="mob-menu__num"
            >
              <span>{{ messagesStore?.totalUnseenMessages }}</span>
            </div>
          </NuxtLink>
        </li>
      </ul>

      <div class="mob-menu__account">
        <div class="mob-menu__account-top">
          <div class="text14 light-text gray-text">Аккаунт</div>
        </div>
        <ul class="mob-menu__links">
          <li>
            <nuxtLink
              to="/profile/settings"
              :active-class="'_active'"
              class="mob-menu__link"
            >
              <svg
                width="18"
                height="18"
                viewBox="0 0 18 18"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  d="M11.0487 7.58205C11.636 7.16121 12.0717 6.5707 12.2937 5.89473C12.5158 5.21877 12.5127 4.49186 12.2851 3.81767C12.0574 3.14348 11.6168 2.55643 11.026 2.14025C10.4352 1.72407 9.72439 1.5 8.99499 1.5C8.26558 1.5 7.5548 1.72407 6.964 2.14025C6.3732 2.55643 5.93256 3.14348 5.70491 3.81767C5.47725 4.49186 5.47422 5.21877 5.69623 5.89473C5.91825 6.5707 6.35397 7.16121 6.94128 7.58205C5.6498 8.00401 4.52676 8.80923 3.73012 9.88444C2.93348 10.9597 2.50332 12.2508 2.50012 13.5762C2.50012 14.2556 2.88263 15.2021 4.70786 15.8565C6.08947 16.3042 7.53896 16.5212 8.99499 16.4984C12.2347 16.4984 15.5001 15.5968 15.5001 13.5837C15.4978 12.2558 15.0669 10.9621 14.2682 9.8852C13.4695 8.80834 12.3433 8.00272 11.0487 7.58205ZM6.55877 4.88218C6.55979 4.41361 6.70353 3.95585 6.97184 3.56673C7.24015 3.17761 7.62099 2.8746 8.06624 2.69597C8.51149 2.51734 9.00117 2.47111 9.47341 2.56313C9.94565 2.65515 10.3793 2.88128 10.7195 3.21296C11.0597 3.54463 11.2912 3.96697 11.3848 4.4266C11.4783 4.88624 11.4298 5.36255 11.2453 5.79535C11.0607 6.22816 10.7485 6.59804 10.3479 6.85826C9.94742 7.11848 9.47661 7.25736 8.99499 7.25736C8.67472 7.25704 8.35766 7.19534 8.0619 7.0758C7.76614 6.95626 7.49748 6.78121 7.27126 6.56065C7.04504 6.3401 6.86568 6.07835 6.74343 5.79036C6.62118 5.50236 6.55843 5.19376 6.55877 4.88218ZM8.99499 15.4993C5.91442 15.4993 3.51671 14.6577 3.51671 13.5837C3.51671 12.1698 4.09402 10.8138 5.12164 9.81408C6.14925 8.81431 7.543 8.25265 8.99627 8.25265C10.4495 8.25265 11.8433 8.81431 12.8709 9.81408C13.8985 10.8138 14.4758 12.1698 14.4758 13.5837C14.4733 14.6577 12.0756 15.4993 8.99499 15.4993Z"
                  fill="#222222"
                />
              </svg>
              <span class="mob-menu__title">Мой профиль</span>
            </nuxtLink>
          </li>
          <li>
            <button :active-class="'_active'" @click="openConfirmLogout">
              <a class="mob-menu__link">
                <svg
                  width="18"
                  height="18"
                  viewBox="0 0 18 18"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    d="M9.82072 9.00793L14.4552 4.3988C14.6773 4.17887 14.6773 3.8228 14.4552 3.60343C14.2335 3.38349 13.8735 3.38349 13.6519 3.60343L9.02141 8.20862L4.34816 3.5348C4.12654 3.31262 3.76654 3.31262 3.54491 3.5348C3.32329 3.75755 3.32329 4.11812 3.54491 4.3403L8.21479 9.01074L3.52804 13.6716C3.30641 13.8916 3.30641 14.2476 3.52804 14.467C3.74966 14.6869 4.10966 14.6869 4.33129 14.467L9.0141 9.81005L13.6688 14.4653C13.8904 14.6875 14.2504 14.6875 14.472 14.4653C14.6937 14.2426 14.6937 13.882 14.472 13.6598L9.82072 9.00793Z"
                    fill="#222222"
                  />
                </svg>
                <span class="mob-menu__title">Выйти</span>
              </a>
            </button>
          </li>
        </ul>
      </div>
    </div>
    <ModulesHeaderMobMenu />
  </header>
</template>

<script setup lang="ts">
import { useAuthStore } from "#imports";
const authStore = useAuthStore();
const messagesStore = useMessagesStore();
const userStore = useUserStore();
const user = defineModel<Profile>("user");
const links = computed(() => {
  return [
    {
      key: "messages",
      path: "/profile/messages",
      title: "Сообщения",
      icon: `<svg
              width="18"
              height="18"
              viewBox="0 0 18 18"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                fill-rule="evenodd"
                clip-rule="evenodd"
                d="M16.4381 1.52184C16.5825 1.65131 16.6437 1.84982 16.5974 2.03813L13.1099 16.2131C13.0595 16.4181 12.8912 16.5729 12.6828 16.6061C12.4744 16.6394 12.2664 16.5447 12.1547 16.3656L8.14372 9.93712L1.73147 7.58048C1.52468 7.50448 1.38734 7.30745 1.38757 7.08714C1.38781 6.86683 1.52558 6.6701 1.73253 6.59454L15.9075 1.41954C16.0897 1.35304 16.2937 1.39237 16.4381 1.52184ZM3.43895 7.08935L8.67493 9.01368C8.78446 9.05394 8.87746 9.12954 8.93924 9.22855L12.3873 14.7549L15.3425 2.74361L3.43895 7.08935Z"
                fill="#222222"
              />
              <path
                fill-rule="evenodd"
                clip-rule="evenodd"
                d="M16.1213 1.87897C16.3263 2.084 16.3263 2.41641 16.1213 2.62144L8.86506 9.87769C8.66003 10.0827 8.32762 10.0827 8.12259 9.87769C7.91757 9.67266 7.91757 9.34025 8.12259 9.13522L15.3788 1.87897C15.5839 1.67395 15.9163 1.67395 16.1213 1.87897Z"
                fill="#222222"
              />
            </svg>`,
    },
  ];
});

messagesStore.fetchTotalUnseenCount();
</script>

<style scoped></style>

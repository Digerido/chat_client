<template>
  <div ref="selectRef" :class="['m-select _multi-select', { _open: isOpen }]">
    <input class="m-select__field" type="hidden" />
    <div class="m-select__toggle" @click="toggleSelect">
      <div class="m-select__current">
        <!-- <template v-for="(option, i) in options" :key="i">
          <div v-if="option.isChecked" class="m-select__tag" @click.stop>
            <span>{{ option.text }}</span>
            <button class="m-select__tag-remove" @click="removeOption(option)">
              <svg
                width="6"
                height="6"
                viewBox="0 0 6 6"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  d="M0.0544632 0.531312L0.594967 0L6 5.31312L5.4595 5.84443L0.0544632 0.531312Z"
                  fill="#222222"
                />
                <path
                  d="M5.40503 0.155566L5.94554 0.686878L0.540503 6L0 5.46869L5.40503 0.155566Z"
                  fill="#222222"
                />
              </svg>
            </button>
          </div>
        </template> -->
      </div>
      <svg
        width="9"
        height="6"
        viewBox="0 0 9 6"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M5.07671 5.33928L8.86404 1.55188C8.9517 1.46428 9 1.34735 9 1.22266C9 1.09798 8.9517 0.981043 8.86404 0.893445L8.58519 0.614529C8.40349 0.433037 8.10818 0.433037 7.92675 0.614529L4.74638 3.7949L1.56248 0.611C1.47482 0.523402 1.35795 0.475036 1.23333 0.475036C1.10858 0.475036 0.991712 0.523402 0.903975 0.611L0.625198 0.889915C0.537531 0.977582 0.489235 1.09445 0.489235 1.21913C0.489235 1.34382 0.537531 1.46075 0.625198 1.54835L4.41599 5.33928C4.50393 5.42709 4.62135 5.47531 4.74617 5.47504C4.87148 5.47531 4.98883 5.42709 5.07671 5.33928Z"
          fill="#041E42"
        />
      </svg>
    </div>
    <div v-if="isOpen" class="m-select__dropdown">
      <!-- <div v-for="option in options" class="m-check" @click="addOption(option)">
        <input
          v-model="option.isChecked"
          :value="option.value"
          type="checkbox"
          @click="option.isChecked"
        />
        <label>
          <span>{{ option.text }}</span>
        </label>
      </div> -->
    </div>
  </div>
</template>

<script setup lang="ts">
const selectRef = ref<HTMLDivElement>();
const props = defineProps({
  options: {
    type: Array,
    required: true,
  },
  placeholder: {
    type: String,
    default: null,
  },
});

const isOpen = ref(false);

onMounted(() => {
  document.addEventListener("click", handleClickOutside);
});

onBeforeUnmount(() => {
  document.removeEventListener("click", handleClickOutside);
});

const toggleSelect = () => {
  isOpen.value = !isOpen.value;
};
// const addOption = (option) => {
//   // isOpen.value = false;
// };
// const removeOption = (option) => {
//   option.isChecked = false;
// };
const handleClickOutside = (event: MouseEvent) => {
  if (selectRef.value && selectRef.value.contains(event.target as Node)) return;
  isOpen.value = false;
};
</script>

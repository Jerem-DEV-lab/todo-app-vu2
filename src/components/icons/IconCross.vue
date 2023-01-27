<template>
  <svg
    xmlns="http://www.w3.org/2000/svg"
    fill="none"
    viewBox="0 0 24 24"
    stroke-width="1.5"
    stroke="currentcolor"
    :height="height"
    :width="width"
  >
    <path
      stroke-linecap="round"
      stroke-linejoin="round"
      d="M6 18L18 6M6 6l12 12"
    />
  </svg>
</template>

<script>
export default {
  name: "icon-cross",
  props: {
    width: {
      default: 24,
    },
    height: {
      default: 24,
    },
  },
};
</script>
